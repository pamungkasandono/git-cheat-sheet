# Git Cheat Sheet: Aman vs Berbahaya Saat Kolaborasi

## Rule of Thumb
> Jangan mengubah riwayat commit yang sudah di-push ke remote jika orang lain mungkin sudah menariknya.

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
