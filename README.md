Analisis Sentimen Ulasan Pengguna Spotify

📌 Overview
Repositori ini berisi implementasi analisis sentimen terhadap ulasan pengguna aplikasi Spotify di Google Play Store. Proyek ini bertujuan untuk:

1. Menganalisis sentimen pengguna terhadap fitur-fitur utama Spotify
2. Mengklasifikasikan ulasan menjadi kategori positif, negatif, atau netral
3. Mengidentifikasi area perbaikan berdasarkan keluhan pengguna

📊 Data Source
Data diperoleh melalui teknik web scraping dari Google Play Store dengan karakteristik:
Sumber Data: Ulasan pengguna aplikasi Spotify
Periode Data: Review terbaru (periode 2023-2025)
Jumlah Data: 3000 ulasan
Metode Pengumpulan: Python google-play-scraper

# kode scraping Spotify
from google_play_scraper import Sort, reviews_all

def scrape_spotify_reviews():
    result = reviews_all(
      'com.spotify.music', # ID aplikasi Spotify
       sleep_milliseconds=0, # delay untuk hindari blokir
       lang='id',
       country='id',
       sort=Sort.MOST_RELEVANT, # urutan berdasarkan relevan
       count=3000,                    #Maksimal permintaan

🔧 Metodologi
1. Preprocessing Data
Cleaning Text: Menghapus URL, emoji, karakter khusus
Music Terminology Handling: Normalisasi istilah musik ("repeat" → "ulang", "shuffle" → "acak")
Stemming: Reduksi kata menggunakan Sastrawi
Stopword Removal: Filter kata tidak penting + istilah khusus musik ("lagu", "musik")

2. Pelabelan Sentimen
def label_sentiment(score):
    if score >= 4:  # Spotify rata-rata rating tinggi
        return "positif"
    elif score <= 2:
        return "negatif"
    else:
        return "netral"

3. Model Machine Learning
        LSTM Classification Report
   
5. Evaluasi Model
   Akurasi: 94.2%
   Presisi:
   Positif: 95%
   Negatif: 78%
   Fitur Paling Berpengaruh:
   Positif: "rekomendasi", "playlist", "kualitas suara"
   Negatif: "iklan", "premium", "buffering"
