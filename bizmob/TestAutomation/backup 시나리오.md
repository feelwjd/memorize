
```python
import pytest, time, json, os

from selenium import webdriver

from selenium.webdriver.common.by import By

from selenium.webdriver.common.action_chains import ActionChains

from selenium.webdriver.support import expected_conditions

from selenium.webdriver.support.wait import WebDriverWait

from selenium.webdriver.common.keys import Keys

from selenium.webdriver.common.desired_capabilities import DesiredCapabilities

from module import screenShot

  

class userManagePage():

"""

화면 요소 ID 설정

"""

input_department = "MVP9000_inp_department"

input_userId = "MVP9000_inp_userId"

input_userNm = "MVP9000_inp_userNm"

button_search = "MVP9000_btn_search"

menu_user_manage = "MVP0111_group_user_manage"

menu_item_user = "MVP0111_item_user"

select_use_yn = "MVP9000_sel_useYn"

select_account_lock = "MVP9000_sel_account_lock"

"""

INPUT 값 설정

"""

val_loginId = "bizmob"

val_loginPw = "12345"

val_department = "사업"

val_userId = "test"

val_userNm = "테스트"

"""

시나리오 1. 사용자 관리 조회

로그인 > 메뉴 선택 > (사용자 관리 > 사용자) > 조회 조건 입력 후 조회

"""

def setup_method(self, test_name):

self.driver = webdriver.Chrome()

self.driver.get("http://218.55.79.67/")

self.vars = {}

self.previous_url = self.driver.current_url # 초기 URL 저장

self.screen_shot = screenShot(self.driver, test_name)

  
  

def teardown_method(self, method):

self.driver.quit()

  

def test_userManageSelect(self):

try:

# 초기 페이지 스크린샷

self.screen_shot.take_screenshot("initial_page")

# 로그인 수행

## 아이디 입력

self.driver.find_element(By.ID, "input-3").click()

self.driver.find_element(By.CSS_SELECTOR, ".v-field--focused .mdi-close-circle").click() #초기화 X 버튼

self.driver.find_element(By.ID, "input-3").send_keys(self.val_loginId)

## 비밀번호 입력

self.driver.find_element(By.ID, "input-5").click()

self.driver.find_element(By.CSS_SELECTOR, ".v-field--focused .mdi-close-circle").click() #초기화 X 버튼

self.driver.find_element(By.ID, "input-5").send_keys(self.val_loginPw)

## 로그인 버튼 클릭

self.driver.find_element(By.CSS_SELECTOR, ".v-btn--block").click()

time.sleep(1)

self.screen_shot.take_screenshot("home_page")

# 메뉴 선택

self.driver.find_element(By.ID, self.menu_user_manage).click()

time.sleep(1)

self.driver.find_element(By.ID, self.menu_item_user).click()

time.sleep(1)

self.screen_shot.take_screenshot("userManage_page")

## 조회 조건 - 부서

self.driver.find_element(By.ID, self.input_department).click()

element = self.driver.find_element(By.CSS_SELECTOR, "#MVP9000_btn_search > .v-btn__content")

actions = ActionChains(self.driver)

actions.move_to_element(element).perform()

self.driver.find_element(By.ID, self.input_department).send_keys(self.val_department)

self.screen_shot.take_screenshot("userManage_page_addDepartment")

## 조회

self.driver.find_element(By.CSS_SELECTOR, "#MVP9000_btn_search > .v-btn__content").click()

time.sleep(1)

## 조회 조건 - 사용자 아이디

self.driver.find_element(By.ID, self.input_userId).click()

element = self.driver.find_element(By.CSS_SELECTOR, "#MVP9000_btn_search > .v-btn__content")

actions = ActionChains(self.driver)

actions.move_to_element(element).perform()

self.driver.find_element(By.ID, self.input_userId).send_keys(self.val_userId)

self.screen_shot.take_screenshot("userManage_page_addUserId")

## 조회

self.driver.find_element(By.CSS_SELECTOR, "#MVP9000_btn_search > .v-btn__content").click()

time.sleep(1)

## 조회 조건 - 사용자 이름

self.driver.find_element(By.ID, self.input_userNm).click()

element = self.driver.find_element(By.ID, self.button_search)

actions = ActionChains(self.driver)

actions.move_to_element(element).perform()

self.driver.find_element(By.ID, self.input_userNm).send_keys(self.val_userNm)

self.screen_shot.take_screenshot("userManage_page_addUserName")

## 조회

self.driver.find_element(By.ID, self.button_search).click()

time.sleep(1)

## 조회 조건 - 사용 여부

element = self.driver.find_element(By.ID, self.button_search)

actions = ActionChains(self.driver)

actions.move_to_element(element).perform()

self.driver.find_element(By.ID, self.select_use_yn).click()

time.sleep(1)

  

# self.driver.find_element(By.CSS_SELECTOR, ".v-field--focused .v-field__input").click()

self.driver.find_element(By.CSS_SELECTOR, ".rounded-0:nth-child(3)").click() #사용 여부 - 사용

## 조회

time.sleep(1)

self.driver.find_element(By.ID, self.button_search).click()

self.screen_shot.take_screenshot("userManage_page_addUserYn")

  

time.sleep(1)

# 조회 조건 - 계정 잠김 여부

# element = self.driver.find_element(By.ID, self.button_search)

# actions = ActionChains(self.driver)

# actions.move_to_element(element).perform()

# self.driver.find_element(By.ID, self.select_account_lock).click()

# self.driver.find_element(By.CSS_SELECTOR, ".rounded-0:nth-child(3)").click() #계정 잠김 - ON

# time.sleep(1)

# 조회

# self.driver.find_element(By.ID, self.button_search).click()

# self.screen_shot.take_screenshot("userManage_page_addAccountLock")

except Exception as e:

print(' Failed to compile, exception is %s' % repr(e))
```