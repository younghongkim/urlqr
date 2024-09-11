import streamlit as st
import pyshorteners
import qrcode
from PIL import Image  # Pillow 라이브러리에서 Image 모듈 가져오기
from io import BytesIO

# 페이지 제목 설정
st.title("URL Shortener with QR Code")

# URL 입력 받기
long_url = st.text_input("Enter the URL to shorten:")

# URL을 줄여주는 함수
def shorten_url(url):
    s = pyshorteners.Shortener()
    return s.tinyurl.short(url)

# QR 코드를 생성하는 함수
def generate_qr_code(url):
    qr = qrcode.QRCode(
        version=1,
        error_correction=qrcode.constants.ERROR_CORRECT_L,
        box_size=10,
        border=4,
    )
    qr.add_data(url)
    qr.make(fit=True)
    img = qr.make_image(fill='black', back_color='white')
    return img

# 버튼을 눌렀을 때 URL 줄이기 및 QR 코드 생성
if st.button("Shorten URL and Generate QR Code"):
    if long_url:
        try:
            # URL 줄이기
            short_url = shorten_url(long_url)
            st.success(f"Shortened URL: {short_url}")

            # QR 코드 생성
            img = generate_qr_code(short_url)
            
            # 이미지를 스트림 형식으로 변환하여 표시
            buf = BytesIO()
            img.save(buf)
            buf.seek(0)
            st.image(buf, caption="QR Code for Shortened URL")

        except Exception as e:
            st.error(f"Error: {str(e)}")
    else:
        st.warning("Please enter a URL to shorten.")
