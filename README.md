# ⚠️ Git Cheat Sheet: Aman vs Berbahaya Saat Kolaborasi

## Rule of Thumb
> Jangan mengubah riwayat commit yang sudah di-push ke remote jika sudah ada orang lain melakukan `git pull`.

---

## Perintah Git Berbahaya Saat Kolaborasi

| Perintah | Apa yang Dilakukan | Masalah Saat Kolaborasi | Alternatif Aman |
|----------|-----------------|------------------------|----------------|
| `git reset --hard <commit>` | Menghapus commit tertentu dari riwayat lokal | Menghapus commit yang sudah di-push bisa menyebabkan riwayat temanmu rusak | Gunakan `git revert <commit>` untuk membatalkan commit tanpa mengubah riwayat |
| `git push --force` / `git push -f` | Memaksa menimpa riwayat di remote | Bisa menghapus commit orang lain yang sudah bekerja di cabang sama | Gunakan `git push --force-with-lease` atau push ke branch baru |
| `git rebase` (terutama `git rebase -i`) | Mengubah riwayat commit (edit, squash, hapus) | Mengubah commit yang sudah di-push menyebabkan konflik besar bagi kolaborator | Lakukan rebase **sebelum push**, atau gunakan merge commit |
| `git commit --amend` setelah push | Mengubah commit terakhir | Jika commit sudah di-push, mengamend dan force push akan mengubah riwayat remote | Commit baru dengan perbaikan (`git commit -m "fix: ..."`) |

---

## Perintah Aman Saat Kolaborasi

| Perintah | Keterangan |
|----------|-----------|
| `git pull` | Mengambil update terbaru dari remote |
| `git merge <branch>` | Menggabungkan branch tanpa mengubah riwayat |
| `git revert <commit>` | Membatalkan commit dengan menambahkan commit baru |
| `git branch <new-branch>` | Membuat branch baru untuk eksperimen |
| `git push` | Push commit baru ke remote tanpa force |

---


# 📌 Git Cheat Sheet: Convenience Commit Message

## Rule of Thumb
> Gunakan commit message yang jelas, konsisten, dan mengikuti aturan *Convenience Commit Message*.  
> Selalu batasi perubahan dalam satu commit pada skala kecil/modul tertentu untuk mempermudah kolaborasi dan review.

---

## 1. Commit Singkat
- **Kapan digunakan:** Untuk perubahan kecil atau tunggal, misal perbaikan typo, style, atau bug minor.
- **Format:** Satu kalimat singkat, present tense, jelas *what changed*.
- **Contoh:**
- **Format yang disarankan:**
  ```
  fix(readme): correct typo in README
  style(ui): adjust button alignment
  chore(api): update endpoint URL
  ```
**Catatan:** Commit kecil membuat riwayat jelas dan mudah di-review.  

---

## 2. Commit Lebih Besar / Banyak Perubahan
- **Kapan digunakan:** Untuk fitur baru, refactor, atau perubahan signifikan.
- **Format yang disarankan:**
  ```
  <type>(<scope>): <subject>
  <body> (optional)
  <footer> (optional)
  ```

- **Penjelasan:**
  - **type:** feat, fix, docs, style, refactor, test, chore  
  - **scope:** modul atau bagian kode yang diubah (opsional)  
  - **subject:** ringkas, maksimal 50 karakter (kira-kira aja), present tense  
  - **body:** penjelasan detail *why* dan *how*, maksimal 72 karakter per baris (kira-kira aja)
  - **footer:** informasi tambahan seperti BREAKING CHANGE atau nomor issue  

- **Contoh:**

  ```
  feat(auth): add JWT token support

  Implemented JWT token generation and verification for login API.
  Added tests for token validation and expiration.

  BREAKING CHANGE: Login API now requires token-based authentication
  ```

**Catatan penting:**

* Usahakan commit dalam **skala kecil/modul tertentu**, jangan digabung menjadi satu commit besar meskipun banyak perubahan.
* Commit besar menyulitkan review, tracking bug, dan revert jika terjadi masalah.
* Selesaikan fitur atau modul kecil dulu, baru commit—riwayat lebih bersih dan kolaborasi lebih aman.

---

## Tipe Commit yang Umum Digunakan (Convenience Commit)

| Type     | Keterangan                                                 | Contoh                            |
| -------- | ---------------------------------------------------------- | ----------------------------------------------- |
| feat     | Fitur baru                                                 | `feat(auth): add login with Google`             |
| fix      | Bug fix                                                    | `fix(ui): correct button alignment`             |
| docs     | Perubahan dokumentasi                                      | `docs(readme): update installation steps`       |
| style    | Format/kode yang tidak mengubah logic (spasi, indent, dll) | `style(navbar): fix indentation and spacing`    |
| refactor | Refactoring kode tanpa menambah fitur atau fix bug         | `refactor(api): simplify request handler logic` |
| test     | Menambah atau memperbaiki test                             | `test(auth): add unit tests for JWT validation` |
| chore    | Perubahan maintenance, build, atau konfigurasi             | `chore(deps): update lodash to v4.17.21`        |
---

## Tips Praktis

* Gunakan **imperative mood**: misal “Add feature” bukan “Added feature”
* Batasi **subject** maksimal 50 karakter
* Body optional, tapi berguna untuk menjelaskan *why* atau *how*
* Gunakan **footer** untuk `BREAKING CHANGE` atau referensi issue
* Konsisten dengan tim agar history mudah dibaca
* **Prioritaskan commit kecil** dan modul spesifik untuk mempermudah kolaborasi
