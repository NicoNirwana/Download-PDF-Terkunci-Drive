# Download-PDF-Terkunci-Drive
Download file pdf yang dilindungi / hanya bisa dilihat dari google drive

1. Buka atau Pratinjau Semua file yang hanya dapat dilihat atau dilindungi dari Google Drive.
2. Buka Console
   -Jika Anda melakukan di Google Chrome atau Firefox
     Tekan Shift + Ctrl + J (di Windows / Linux) atau Option + ⌘ + J (di Mac)
   -Jika Anda melakukan di Microsoft Edge
     Tekan Shift + Ctrl + I
   -Jika Anda melakukan di Apple Safari
     Tekan Opsi + ⌘ + C
   
   Kemudian kamu akan melihat Navigasi dari inspect Element

3 Navigasikan ke tab "Consol".
4 Pastikan kamu scrol halaman secara perlahan sampai di halaman akhir pdf, agar semua file dapat terbaca dan tidak ada yg tertinggal
5 Paste kode di bawah ini dan tekan Enter:

let jspdf = document.createElement( "script" );
jspdf.onload = function () {
let pdf = new jsPDF();
let elements = document.getElementsByTagName( "img" );
for ( let i in elements) {
let img = elements[i];
if (!/^blob:/.test(img.src)) {
continue ;
}
let canvasElement = document.createElement( 'canvas' );
let con = canvasElement.getContext( "2d" );
canvasElement.width = img.width;
canvasElement.height = img.height;
con.drawImage(img, 0, 0,img.width, img.height);
let imgData = canvasElement.toDataURL( "image/jpeg" , 1.0);
pdf.addImage(imgData, 'JPEG' , 0, 0);
pdf.addPage();
}
pdf.save( "download.pdf" );
};
jspdf.src = 'https://cdnjs.cloudflare.com/ajax/libs/jspdf/1.3.2/jspdf.min.js' ;
document.body.appendChild(jspdf);
