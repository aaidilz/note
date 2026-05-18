# Project: defend.azharmtq.my.id (Code:AZR:2026)

**Status: disclosed`**  
**Generated Date: `16 May 2026`**

---

# 1. Executive Summary

Assessment dilakukan terhadap target `defend.azharmtq.my.id` yang menjalankan platform WordPress 6.9.4 dengan konfigurasi default dan perlindungan Cloudflare WAF. Hasil pengujian menunjukkan beberapa area yang meningkatkan attack surface, terutama pada XML-RPC exposure, REST API disclosure, dan kelemahan hardening dasar WordPress.

Tidak ditemukan indikasi eksploitasi aktif ataupun compromise selama pengujian berlangsung. Namun, beberapa konfigurasi memungkinkan enumerasi informasi sensitif yang dapat digunakan sebagai tahap awal serangan lanjutan seperti credential stuffing, brute-force amplification, maupun reconnaissance terhadap environment WordPress.

---

# 2. Assets in Scope

## Domain
1. defend.azharmtq.my.id

---

# 3. Vulnerability Findings

## 3.1 XML-RPC Full Exposure - `/xmlrpc.php`

| Severity | High (CVSS: 8.6)                             |
| -------- | -------------------------------------------- |
| Status   | Open                                         |
| Category | A05:2021-Security Misconfiguration           |
| Vector   | CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:N/I:N/A:H |

### Description

| Target  | https://defend.azharmtq.my.id/xmlrpc.php |
| ------- | ---------------------------------------- |
| Tanggal | 16 May 2026 |
| Penguji | Null |

**Background**  
xmlrpc.php adalah file inti (core) WordPress yang berfungsi sebagai jembatan komunikasi jarak jauh. Fitur ini memungkinkan aplikasi luar atau sistem lain (seperti aplikasi mobile WordPress atau layanan pingback) untuk bertukar data dan mengelola situs web Anda secara otomatis.

Secara default XML-RPC sering menjadi target abuse karena mendukung metode seperti `system.multicall` dan `pingback.ping`.

**Objective**  
Melakukan identifikasi apakah endpoint XML-RPC masih aktif dan mengevaluasi metode yang tersedia untuk kemungkinan abuse terhadap authentication mechanism maupun amplification attack.

**Impact**  
Endpoint XML-RPC ditemukan aktif dan mengekspos lebih dari 80 metode bawaan WordPress. Metode `system.multicall` memungkinkan attacker melakukan banyak percobaan autentikasi dalam satu request sehingga dapat mempercepat brute-force attack dan mem-bypass sebagian rate limiting tradisional.

Selain itu metode `pingback.ping` berpotensi digunakan sebagai SSRF ataupun DDoS reflection vector. Kombinasi user enumeration dan XML-RPC authentication dapat meningkatkan risiko credential attack terhadap akun administrator.

**Reproduction Steps**

1. Mengirim request POST ke endpoint:
```http
   POST /xmlrpc.php HTTP/2
   Host: defend.azharmtq.my.id
   Content-Type: text/xml
```

2. Menggunakan payload XML:

```bash
curl -X POST "https://target.com/xmlrpc.php" \
  -H "Content-Type: text/xml" \
  --data '<?xml version="1.0"?>
<methodCall>
    <methodName>system.listMethods</methodName>
    <params></params>
</methodCall>'
```

3. Server merespons daftar method XML-RPC yang tersedia.

| Category             | Methods                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| -------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **System**           | system.multicall, system.listMethods, system.getCapabilities                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| **Pingback**         | pingback.ping, pingback.extensions.getPingbacks                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| **Blogger API**      | blogger.getUsersBlogs, blogger.getUserInfo, blogger.getPost, blogger.getRecentPosts, blogger.newPost, blogger.editPost, blogger.deletePost                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| **MetaWeblog API**   | metaWeblog.getUsersBlogs, metaWeblog.getCategories, metaWeblog.getPost, metaWeblog.getRecentPosts, metaWeblog.newPost, metaWeblog.editPost, metaWeblog.deletePost, metaWeblog.newMediaObject                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| **Movable Type API** | mt.getCategoryList, mt.getPostCategories, mt.setPostCategories, mt.supportedMethods, mt.supportedTextFilters, mt.getTrackbackPings, mt.publishPost                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| **WordPress API**    | wp.getUsersBlogs, wp.getUser, wp.getUsers, wp.getProfile, wp.editProfile, wp.getAuthors, wp.getPage, wp.getPages, wp.newPage, wp.editPage, wp.deletePage, wp.getPageList, wp.getPost, wp.getPosts, wp.newPost, wp.editPost, wp.deletePost, wp.getPostType, wp.getPostTypes, wp.getPostFormats, wp.getPostStatusList, wp.getPageStatusList, wp.getPageTemplates, wp.getTaxonomy, wp.getTaxonomies, wp.getTerm, wp.getTerms, wp.newTerm, wp.editTerm, wp.deleteTerm, wp.getCategories, wp.getTags, wp.suggestCategories, wp.newCategory, wp.deleteCategory, wp.getComment, wp.getComments, wp.newComment, wp.editComment, wp.deleteComment, wp.getCommentCount, wp.getCommentStatusList, wp.getOptions, wp.setOptions, wp.getMediaItem, wp.getMediaLibrary, wp.uploadFile, wp.deleteFile, wp.getRevisions, wp.restoreRevision |

Endpoint merespons valid XML response dan menampilkan method yang Kritikal

| Risk                 | Detail                                          |
| -------------------- | ----------------------------------------------- |
| **system.multicall** | Vektor Enable Brute Force untuk 1 permintaan    |
| **pingback.ping**    | Potensi vektor SSRF dan amplifikasi DDoS        |
| **wp.uploadFile**    | Kemampuan upload file (membutuhkan autentikasi) |
| **wp.***             | API manajemen penuh WordPress terekspos         |

---

## 3.2 REST API User Enumeration - `/wp-json/wp/v2/users`

| Severity | 5.3 (Medium)                                 |
| -------- | -------------------------------------------- |
| Status   | Open                                         |
| Category | A01:2021-Broken Access Control               |
| Vector   | CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:L/I:N/A:N |

### Description

| Target  | [https://defend.azharmtq.my.id/wp-json/wp/v2/users](https://defend.azharmtq.my.id/wp-json/wp/v2/users) |
| ------- | ------------------------------------------------------------------------------------------------------ |
| Tanggal | 16 May 2026                                                                                            |
| Penguji | Null                                                                                                   |

**Background**
REST API WordPress secara default dapat mengekspos informasi user publik apabila tidak dilakukan pembatasan akses tambahan.

**Objective**
Melakukan validasi apakah endpoint REST API dapat digunakan untuk enumerasi user WordPress.

**Impact**
Endpoint `/wp-json/wp/v2/users` dapat diakses tanpa autentikasi dan mengungkap username administrator `kotatsu` beserta metadata terkait.

Informasi ini dapat digunakan attacker untuk:

* username enumeration
* targeted password attack
* credential stuffing
* spear phishing
* correlation terhadap akun lain

**Reproduction Steps**

1. Akses endpoint:

   ```http
   GET /wp-json/wp/v2/users HTTP/2
   Host: defend.azharmtq.my.id
   ```

2. Server mengembalikan response JSON:

   ```json
   [
      {
         "id":1,
         "name":"kotatsu",
         "slug":"kotatsu"
      }
   ]
   ```


Endpoint dapat diakses tanpa authentication dan menampilkan data user WordPress.

---

## 3.3 Sensitive File Disclosure - `/readme.html`

| Severity | 5.3 (Medium)                                 |
| -------- | -------------------------------------------- |
| Status   | Open                                         |
| Category | A02:2025-Security Misconfiguration           |
| Vector   | CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:L/I:N/A:N |

### Description

| Target  | [https://defend.azharmtq.my.id/readme.html](https://defend.azharmtq.my.id/readme.html) |
| ------- | -------------------------------------------------------------------------------------- |
| Tanggal | 16 May 2026                                                                            |
| Penguji | Null                                                                                   |

**Background**
File default WordPress seperti `readme.html` sering kali berisi informasi mengenai versi WordPress dan stack requirement.

**Objective**
Mengidentifikasi file bawaan WordPress yang masih dapat diakses publik.

**Impact**
File `readme.html` dapat diakses secara publik dan mengungkap penggunaan WordPress beserta informasi versi environment yang direkomendasikan.

Walaupun dampaknya terbatas, informasi ini dapat membantu attacker dalam fingerprinting dan pemetaan target sebelum eksploitasi lanjutan.

**Reproduction Steps**

1. Akses:

```bash
curl -X GET "https://defend.azharmtq.my.id/readme.html" \
--http2 \
-H "Host: defend.azharmtq.my.id"
```

2. Server menampilkan halaman readme bawaan WordPress.

---

# 4. Conclusion

Hasil assessment menunjukkan bahwa target masih menggunakan konfigurasi WordPress yang relatif default dengan beberapa mekanisme hardening yang belum diterapkan secara optimal. Walaupun tidak ditemukan indikasi remote code execution ataupun compromise aktif, kombinasi antara XML-RPC exposure, REST API disclosure, dan minimnya proteksi autentikasi dapat meningkatkan risiko terhadap brute-force attack dan reconnaissance lanjutan.

---

# 5. Reference

* [OWASP Top 10 2025](https://owasp.org/Top10/2025/)
* [WordPress Hardening Documentation](https://developer.wordpress.org/advanced-administration/security/hardening/)
* [CVSS v3.1 Specification](https://www.first.org/cvss/calculator/3.1) 

---

Report generate by Null