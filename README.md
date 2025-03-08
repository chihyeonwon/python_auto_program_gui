# python_auto_program_gui
업무 자동화 프로그램 파이썬 필요한 공부 

```
import pygetwindow as gw
import pyautogui
from PIL import ImageGrab
import time

def get_taskbar_coordinates():
    """작업 표시줄의 좌표를 찾는 함수"""
    for window in gw.getWindowsWithTitle("작업 표시줄"):  # 작업 표시줄 찾기
        return window.left, window.top, window.width, window.height
    return None

def get_pixel_color(x, y):
    """주어진 좌표의 픽셀 색상을 반환하는 함수"""
    img = ImageGrab.grab(bbox=(x, y, x+1, y+1))  # 특정 좌표 1픽셀만 캡처
    color = img.getpixel((0, 0))  # 픽셀 색상 추출
    return color  # RGB 값 반환

# 실행
taskbar = get_taskbar_coordinates()
if taskbar:
    left, top, width, height = taskbar
    print(f"작업 표시줄 좌표: 왼쪽 {left}, 상단 {top}, 너비 {width}, 높이 {height}")
    
    # 작업 표시줄 중앙 부분의 색상 가져오기
    x, y = left + width // 2, top + height // 2
    color = get_pixel_color(x, y)
    print(f"작업 표시줄 중앙 색상 (RGB): {color}")

else:
    print("작업 표시줄을 찾을 수 없습니다.")
if color == (0, 120, 215):  # 예: Windows 기본 아이콘 색상
    print("파란색 아이콘이 감지되었습니다!")
```
