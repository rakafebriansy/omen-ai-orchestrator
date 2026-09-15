# Retrospectives Directory (`retrospectives/`) — Omen

Direktori ini adalah pusat **Evaluasi Diri (Self-Healing) AI Agent**. Tujuan utama folder ini adalah untuk melacak, mencatat, dan menganalisis setiap kesalahan, halusinasi, atau keputusan keliru yang dilakukan oleh AI selama siklus pengembangan berlangsung di node Omen.

## Cara Kerja Workflow Retrospective
1. **Pencatatan Masalah:** Saat AI Agent menemui hambatan teknis kronis, gagal memperbaiki *bug*, atau ditegur oleh pengguna, AI **WAJIB** mencatat kejadian tersebut ke dalam file `RETROSPECTIVE.md`.
2. **Pencatatan Resolusi Konflik (Merge):** Apabila terjadi proses *merge branch*, catat resolusi ke `MERGE_HISTORY.md`.
3. **Konversi ke Aturan Konkret:** Catatan evaluasi dikonversi menjadi aturan baku di `guidelines/project-context.md`.
