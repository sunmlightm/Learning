#### Selenium与PhantomJS
1. PhantomJS是一个无界面浏览器
2. Selenium:是一个web自动化测试工具,可以按照指定的命令自动操作

**快速入门**
- from selenium import webdriver # 导入webdriver
- from selenium.webdriver.common.keys import Keys # 导入键盘操作keys包
- driver = webdriver.PhantomJS(executable_path="./phantomjs")) # 创建PhantomJS浏览器创建浏览器对象
- driver = webdriver.Chrome() #创建chrome浏览器对象
    - **创建chrome无头浏览器**:
    - from  selenium.webdriver.chrome.options import Options
    - SERVICE_ARGS = ['--load-images=false', '--disk-cache=false'] #设置不缓存
    - chrome_options=Options()
    - chrome_options.add_argument('--headless')
    - driver = webdriver.Chrome(chrome_options=chrome_options,service_args=SERVICE_ARGS)
    - 

#创建浏览器对象
# driver = webdriver.Chrome()
driver = webdriver.Chrome(service_args=SERVICE_ARGS)

- driver.get("http://www.baidu.com/") # 请求页面
- data = driver.find_element_by_id("wrapper").text # 获取页面数据
- "print driver.title # 打印页面标题
- driver.save_screenshot("baidu.png") 保存当前页面快照
- driver.find_element_by_id("kw").send_keys(u"长城") # 模拟输入
- driver.find_element_by_id("su").click() # 模拟点击
- print driver.page_source # 打印网页渲染后的源代码
- print driver.get_cookies() # 获取当前页面的Cookie
- driver.find_element_by_id("kw").send_keys(Keys.CONTROL,'a') #全选'kw'中的内容
    - send_keys(Keys.CONTROL,'x')  #剪切
    - send_keys("atguigu") # 重新输入字符串'atguigu'
    - send_keys(Keys.RETURN) # 模拟回车键
- driver.find_element_by_id("kw").clear() # 清除输入框内容
- print driver.current_url # 获取当前url
- driver.close() # 关闭当前页面,如果只有一个页面则关闭浏览器
- driver.quit() # 关闭浏览器

---
**页面操作**

- 定位UI元素:
    - find_element_by_id("id_name") # 获取id标签
    - find_elements_by_name()
    - find_elements_by_xpath() # 通过XPath语法获取
    - find_elements_by_link_text # 通过a标签中的text获取
    - find_elements_by_partial_link_text (作用与by_link_text相同)
    - find_elements_by_tag_name # 通过标签名
    - find_elements_by_class_name
    - find_elements_by_css_selector() (类名中有空格时需要使用点代替)
    - 用法实例:
        1. 第一种: cheese = driver.find_element_by_css_selector("#food span.dairy.aged")
        2. 第二种:
        2. from selenium.webdriver.common.by import By
        3. cheese = driver.find_element(By.CSS_SELECTOR, "#food span.dairy.aged")

**鼠标动作链**
- from selenium.webdriver import ActionChains 导入 ActionChains 类
- ac = driver.find_element_by_xpath('element') # 获取元素
- ActionChains(driver).move_to_element(ac).perform() # 鼠标移动到ac位置
- ActionChains(driver).move_to_element(ac).click(ac).perform()在ac位置单击
- ActionChains(driver).move_to_element(ac).double_click(ac).perform() #双击
- ActionChains(driver).move_to_element(ac).context_click(ac).perform() 右击
- ActionChains(driver).move_to_element(ac).click_and_hold(ac).perform() 点住不放
- ActionChains(driver).drag_and_drop(ac1, ac2).perform() 将ac1拖动到ac2的位置

**填充表格**
- from selenium.webdriver.support.ui import Select # 导入select模块处理表格select = Select(driver.find_element_by_name('status')) # 获取选项卡
- select.select_by_index(1) 根据下标选取 从0开始
- select.select_by_value("3") 根据value值选取
- select.select_by_visible_text("审核不通过") 根据显示的值选取
- select.deselect_all() 全部取消选择

**弹窗处理**
- alert = driver.switch_to_alert() 定位到弹窗

**页面切换**
- driver.switch_to.window("this is window name")
- for handle in driver.window_handles:
    - driver.switch_to_window(handle)
    -获取每个窗口的操作对象

**页面前进后退**
- driver.forward()
- driver.back()

**Cookies**
- 获取页面每个cookies:
> 
    for cookie in driver.get_cookies():
        print "%s -> %s" % (cookie['name'], cookie['value'])

- 删除Cookies
    - driver.delete_cookie("CookieName")
    - driver.delete_all_cookies()

**页面等待**
- 原因:现在的网页越来越多采用了 Ajax 技术，这样程序便不能确定何时某个元素完全加载出来了
- 方法:隐式等待是等待特定的时间，显式等待是指定某一条件直到这个条件成立时继续执行。

> 
    #显式等待
    from selenium import webdriver
    from selenium.webdriver.common.by import By# WebDriverWait 库，负责循环等待
    from selenium.webdriver.support.ui import WebDriverWait# expected_conditions 类，负责条件出发
    from selenium.webdriver.support import expected_conditions as EC
    
    driver = webdriver.Chrome()
    driver.get("http://www.xxxxx.com/loading")
    try:
        # 页面一直循环，直到 id="myDynamicElement" 出现
        element = WebDriverWait(driver, 10).until(
            EC.presence_of_element_located((By.ID, "myDynamicElement"))
        )finally:
        driver.quit()
    ----------------------------------------------------
    # 隐式等待
    from selenium import webdriver
    driver = webdriver.Chrome()
    driver.implicitly_wait(10) # seconds
    driver.get("http://www.xxxxx.com/loading")
    myDynamicElement = driver.find_element_by_id("myDynamicElement")

--------------
**测试模块**
> 
    import time
    #导入python测试模块
    import unittest
    #类名任意,但必须继承unittest.TestCase
    class DouyuTest(unittest.TestCase):
       #固定写法,通常做初始化
       def setUp(self):
          print("setUp()....")
          self.num1 = 1
          self.num2 = 1
       def testTest(self):
          for i in range(1,3):
             print("testTest()==",i)
             self.num1 += 1
             time.sleep(1)
       def testTest2(self):
          for i in range(1,3):
             print("testTest2()==",i)
             self.num2 += 1
             time.sleep(1)
       #固定写法,但每个自定义方法接收后都会调用一次该方法
       def tearDown(self):
          print("tearDown()...")
          print("num1==",self.num1)
          print("num2==", self.num2)
    if __name__ == "__main__":
       #调用的时候只需要写上main,固定的调用方式
       unittest.main()
