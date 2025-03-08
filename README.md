# python_auto_program_gui
업무 자동화 프로그램 파이썬 필요한 공부 

작업표시줄 위에 떠 있는 아이콘의 위치를 계산
```python
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
단축키 자동화 python
```
import keyboard

# 특정 단축키 차단 (예: Ctrl+C, Alt+Tab)
block_keys = ["ctrl+c", "alt+tab", "win+d"]

def block_hotkeys(event):
    if event.name in block_keys:
        print(f"{event.name} 단축키가 차단되었습니다.")
        return False  # 입력 차단

# 키 이벤트 감지하여 차단
for key in block_keys:
    keyboard.block_key(key)

# 사용자 정의 단축키 설정
def custom_function():
    print("Ctrl+Shift+S 단축키가 감지되었습니다! 원하는 기능을 실행하세요.")

keyboard.add_hotkey("ctrl+shift+s", custom_function)  # Ctrl+Shift+S 입력 시 실행

print("단축키 감지가 시작되었습니다. 종료하려면 Ctrl+C를 누르세요.")
keyboard.wait("esc")  # ESC 키를 누를 때까지 실행 유지
```

복사, 붙여넣기 자동화
