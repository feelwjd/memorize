## 목차
1. 프로젝트 구조
2. 설치 방법
3. 환경 설정
4. 모듈 및 구성 요소
5. 프로젝트 실행 방법
6. 스크린샷 저장 및 확인
7. 확장 및 커스터마이징
---
# 1. 프로젝트 구조
```bash
├── app.py.               # 메인 실행 파일
├── config.py             # 설정 파일
├── module                # 모듈 폴더
│   ├── __init__.py       # 모듈 초기화 파일
│   └── screenshot.py     # 스크린샷 모듈 파일
├── screenShot            # 시나리오 테스트 별 스크린샷 모음 폴더
│   └── test_userManageSelect
│       ├── step_1_initial_page.png
│       ├── step_2_home_page.png
│       ├── step_3_userManage_page.png
│       ├── ...
├── testCases
│   ├── senarioTest       # 시나리오 테스트 관리 폴더
│   │   └── userManagePage.py
│   └── unitTest          # 단위 테스트 관리 폴더
│       ├── login.py
│       ├── menu_select.py
│       └── search.py
└── requirements.txt           # pip 의존성 목록 리스트 파일
```

---
# 2. 설치 방법
- Python 3.7 이상
- [Chrome 브라우저 및 ChromeDriver 설치](https://developer.chrome.com/docs/chromedriver/downloads?hl=ko)
- Python 가상 환경 구성
```bash
cd <프로젝트 디렉토리>
python -m venv .venv   #venv 가상 환경 폴더 생성

---
# 가상환경 활성화
source .venv/bin/activate. # 리눅스 기반 OS
.venv\Scripts\activate.    # Windows os
```
- 필요한 Python 패키지 설치:
```bash
pip install -r requirements.txt
```

---
# 3. 환경 설정
### 3.1 `.env` 파일 설정
`userManagePage.py`에서 환경 변수로 테스트할 URL을 읽어옵니다. 
프로젝트 루트 디렉토리에 `.env` 파일을 생성합니다.
```env
TEST_URL=http://테스트할-웹페이지-주소
```

### 3.2 스크린샷 저장 경로
`config.py` 파일에서 기본 스크린샷 저장 경로를 설정합니다.
```python
baseDir = "./screenShot"
```

---
# 4. 모듈 및 구성 요소
### 4.1 `app.py`
프로젝트의 메인 실행 파일로, 특정 테스트 케이스를 호출하여 실행합니다.

```python
from testCases.senarioTest.userManagePage import userManagePage

  

def main():

	test_class = userManagePage()
	
	test_class.setup_method("test_userManageSelect")
	
	test_class.test_userManageSelect()
	
	test_class.teardown_method()

  

if __name__ == "__main__":
	main()
```
setup.method() 함수를 통해서 테스트 명을 입력하게 되면, 해당 테스트 이름의 스크린샷 폴더가 생성되고 테스트 진행 중 스크린샷 찍은 png 파일들이 저장됩니다.

### 4.2 `screenShot.py`
프로젝트의 스크린샷 모듈 파일로, 테스트 도중 스크린샷을 찍어주는 기능을 합니다.
```python
import time, os

from config import baseDir

  

class screenShot:

	def __init__(self, driver, test_name):
	
		self.driver = driver
		
		self.screenshot_step = 1
		
		self.folder_path = os.path.join(baseDir, test_name)
	
		# 폴더가 없으면 생성
		
		if not os.path.exists(self.folder_path):
		
			os.makedirs(self.folder_path)
	
	  
	
	def take_screenshot(self, action_description):
	
		time.sleep(2)
		
		file_path = f"{self.folder_path}/step_{self.screenshot_step}_{action_description}.png"
		
		self.driver.save_screenshot(file_path)
		
		self.screenshot_step += 1
	
	# 네비게이션 테스트 때 수행
	
	def check_url_change_and_capture(self, action_description):
	
		current_url = self.driver.current_url
		
		if current_url != self.previous_url:
			
			self.take_screenshot(action_description)
			
			self.previous_url = current_url # 업데이트된 URL로 설정
```

`take_screenshot` 함수를 호출 하면 2초의 시간을 기다렸다가 화면을 촬영합니다.
`check_url_change_and_capture` 함수를 호출하면 페이지 url 변화가 있을 때 마다 화면 촬영합니다. 


### 4.3 단위 테스트

**로그인 단위 테스트**
- 스크린샷 모듈을 상속받아 초기화를 한 후 단위 테스트 내에서 스크린샷 기능을 사용할 수 있게 합니다.
- input 값을 `perform_login()`의 인자 값으로 받아 동적으로 테스트 수행할 수 있게 합니다.
```python
from selenium.webdriver.common.by import By

import time

  

class Login:

	def __init__(self, driver, screen_shot):
	
		self.driver = driver
		
		self.screen_shot = screen_shot
	
	  
	
	def perform_login(self, login_id, login_pw):
	
		self.screen_shot.take_screenshot("initial_page")
		
		self.driver.find_element(By.ID, "input-3").click()
		
		self.driver.find_element(By.CSS_SELECTOR, ".v-field--focused .mdi-close-circle").click()
		
		self.driver.find_element(By.ID, "input-3").send_keys(login_id)
		
		self.driver.find_element(By.ID, "input-5").click()
		
		self.driver.find_element(By.CSS_SELECTOR, ".v-field--focused .mdi-close-circle").click()
		
		self.driver.find_element(By.ID, "input-5").send_keys(login_pw)
		
		self.driver.find_element(By.CSS_SELECTOR, ".v-btn--block").click()
		
		time.sleep(1)
		
		self.screen_shot.take_screenshot("home_page")
```

위와 같이 각각의 단위 기능의 테스트를 수행할 수 있도록 소스를 작성 후 시나리오 테스트에서 호출 할 수 있도록 합니다.

### 4.4 시나리오 테스트
### **주요 시나리오**

특정 페이지에서 단위 테스트에서 작성한 기능들을 자동화합니다.

*예시*
1. **로그인**: 제공된 사용자 ID와 비밀번호로 로그인.
2. **메뉴 선택**: "사용자 관리" 메뉴와 하위 메뉴를 선택.
3. **조회 조건 입력 및 확인**: 다양한 조회 조건(부서, 사용자 ID, 이름 등)을 입력하여 필터링 된 결과를 확인.
4. **페이징 테스트**: 페이지 전환 및 항목 수 변경 기능을 테스트.

```python
from module import screenShot
# .... 모듈 호출
import os

  

# load .env
load_dotenv()

  

"""

시나리오 : 사용자 관리 조회

로그인 > 메뉴 선택 > (사용자 관리 > 사용자) > 조회 조건 입력 후 조회

"""

class userManagePage:

	"""
	
	화면 요소 ID 설정
	
	"""

	input_department = "MVP9000_inp_department"
	
	input_userId = "MVP9000_inp_userId"
	
	input_userNm = "MVP9000_inp_userNm"
	
	button_search = "MVP9000_btn_search"
	
	...
	
	"""
	
	INPUT 값 설정
	
	"""
	
	val_loginId = "bizmob"
	
	val_loginPw = "12345"
	
	...
	
	test_url = os.getenv('TEST_URL')
	
	  
	
	def setup_method(self, test_name):
	
		chrome_options = Options()
		
		chrome_options.add_argument("window-size=1920,1080")
		
		self.driver = webdriver.Chrome(options=chrome_options)
		
		self.driver.get(self.test_url)
		
		self.screen_shot = screenShot(self.driver, test_name)
	
		"""
		
		테스트 수행 클래스 호출
		
		"""
		
		self.login = Login(self.driver, self.screen_shot)
		
		self.menu_select = MenuSelect(self.driver, self.screen_shot)
		
		self.search = Search(self.driver)
	
	  
	
	def teardown_method(self):
	
		self.driver.quit()
	
	  
	
	def test_userManageSelect(self):
	
		try:
	
			#로그인
	
			self.login.perform_login(self.val_loginId, self.val_loginPw)
			
			#메뉴 선택
			
			self.menu_select.select_user_manage_menu(self.menu_user_manage, self.menu_item_user)
			
			#사용자 조회
			
			## 조회 조건 - 부서
			
			self.search.perform_input(self.input_department, self.val_department)
			
			self.driver.find_element(By.ID, self.button_search).click()
			
			
			## 조회 조건 - 사용자 아이디
			
			self.search.perform_input(self.input_userId, self.val_userId)
			
			self.driver.find_element(By.ID, self.button_search).click()
			
			
			## 조회 조건 - 사용자 이름
			
			self.search.perform_input(self.input_userNm, self.val_userNm)
			
			self.driver.find_element(By.ID, self.button_search).click()
			
			
			## 조회 조건 - 사용 여부
			
			self.search.perform_list(self.select_use_yn, self.select_list_second)
			
			self.driver.find_element(By.ID, self.button_search).click()
			
			
			## 조회 조건 - 잠김 여부
			
			self.search.perform_list(self.select_lock_lock, self.select_list_third)
			
			self.driver.find_element(By.ID, self.button_search).click()
			
			
			## 조회 조건 - 삭제 여부
			
			self.search.perform_list(self.select_delete_yn, self.select_list_third)
			
			self.driver.find_element(By.ID, self.button_search).click()
			
			
			# 조회 조건 초기화
			
			self.search.perform_input(self.input_department, "")
			
			self.search.perform_input(self.input_userId, "")
			
			self.search.perform_input(self.input_userNm, "")
			
			self.search.perform_list(self.select_use_yn, self.select_list_first)
			
			self.search.perform_list(self.select_lock_lock, self.select_list_first)
			
			self.search.perform_list(self.select_delete_yn, self.select_list_first)
			
			self.driver.find_element(By.ID, self.button_search).click()
			
			## 조회 조건 - 페이지네이션
			
			self.search.perform_list(self.select_item_perPage, self.select_list_first)
			
			
			## 조회 조건 - 2번 탭
			
			self.driver.find_element(By.CSS_SELECTOR, self.select_page_second).click()
			
			
			## 조회 조건 - 1번 탭
			
			self.driver.find_element(By.CSS_SELECTOR, self.select_page_first).click()
			
			
			## 조회 조건 - 다음 페이지
			
			self.driver.find_element(By.CSS_SELECTOR, self.select_page_next).click()
			
			
			## 조회 조건 - 이전 페이지
			
			self.driver.find_element(By.CSS_SELECTOR, self.select_page_prev).click()
			
	
		except Exception as e:
	
			print(' Failed to compile, exception is %s' % repr(e))
```

시나리오 테스트 클래스 안에 `화면 요소 ID`와 `input 값` 을 지정한 후 단위 테스트 클래스를 호출하여 수행할 수 있도록 합니다.

---
# 5. 프로젝트 실행 방법
1. `.env`파일을 생성하고 `TEST_URL` 을 설정합니다.
2. 가상 파이썬 환경을 이용하고 있는지 확인합니다.
```bash
python --version
```
3. 프로젝트를 실행합니다.
```bash
python app.py
```

---
# 6. 스크린샷 저장 및 확인
테스트 실행 시 각 단계별로 스크린샷이 저장됩니다. 스크린샷은 `config.py`에서 설정한 경로에 `테스트_이름/step_번호_설명.png` 형식으로 저장됩니다.

예:
```bash
screenShot/
├── test_userManageSelect/
│   ├── step_1_initial_page.png
│   ├── step_2_home_page.png
│   ├── ...
```

---
# 7. 확장 및 커스터마이징
### 7.1 새로운 테스트 케이스 추가

- `testCases/senarioTest` 디렉토리에 새로운 테스트 클래스를 추가합니다.
- `setup_method`와 `teardown_method`를 재사용하여 설정과 종료를 구성합니다.

### 7.2 추가 기능 구현

- 새로운 페이지 동작이 필요하면 `unitTest` 디렉토리에 테스트 케이스를 추가하여 캡슐화된 기능을 구현합니다.
