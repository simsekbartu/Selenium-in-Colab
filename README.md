# 🖥 Selenium Webdriver in Google Colab
After successfully installing Selenium using the command `!pip install selenium`, 
```bash
# Install Selenium
!pip install selenium
```
if `NoSuchDriverException` issue arises when trying to run this kind of code,
```bash
from selenium import webdriver
from selenium.webdriver.chrome.options import Options
from selenium.webdriver.chrome.service import Service
import time

# Basic example
url = "https://pubchem.ncbi.nlm.nih.gov/#query=586-76-5"
service = Service("/usr/bin/chromedriver")
options = Options()
options.add_argument("--headless")
options.add_argument("--no-sandbox")
driver = webdriver.Chrome(service=service, options=options)
driver.get(url)
print(driver.title)
```
`NoSuchDriverException` occurs when Selenium is unable to locate or obtain the appropriate driver for the specified browser (in this case, `Chrome`):
```bash
---------------------------------------------------------------------------
NoSuchDriverException                   Traceback (most recent call last)
<ipython-input-8-af9443d39392> in <cell line: 16>()
     14 options.add_argument("--no-sandbox")
     15 
---> 16 driver = webdriver.Chrome(service=service, options=options)
     17 
     18 driver.get(url)

2 frames
/usr/local/lib/python3.10/dist-packages/selenium/webdriver/common/driver_finder.py in get_path(service, options)
     42 
     43         if path is None or not Path(path).is_file():
---> 44             raise NoSuchDriverException(f"Unable to locate or obtain driver for {options.capabilities['browserName']}")
     45 
     46         return path

NoSuchDriverException: Message: Unable to locate or obtain driver for chrome; For documentation on this error, please visit: https://www.selenium.dev/documentation/webdriver/troubleshooting/errors/driver_location
```
# 🛠 Solution

<a href="https://colab.research.google.com/github/simsekbartu/Selenium-in-Colab/blob/main/Selenium_Webdriver_in_Google_Colab.ipynb" target="_blank">
    <img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/>
</a>

Prior to employing your code, you can seamlessly initiate the use of `Selenium` in **Google Colab** by employing the provided "**shell**" below.
```bash
%%shell
cat > /etc/apt/sources.list.d/debian.list <<'EOF'
deb [arch=amd64 signed-by=/usr/share/keyrings/debian-buster.gpg] http://deb.debian.org/debian buster main
deb [arch=amd64 signed-by=/usr/share/keyrings/debian-buster-updates.gpg] http://deb.debian.org/debian buster-updates main
deb [arch=amd64 signed-by=/usr/share/keyrings/debian-security-buster.gpg] http://deb.debian.org/debian-security buster/updates main
EOF
apt-key adv --keyserver keyserver.ubuntu.com --recv-keys DCC9EFBF77E11517
apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 648ACFD622F3D138
apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 112695A0E562B32A

apt-key export 77E11517 | gpg --dearmour -o /usr/share/keyrings/debian-buster.gpg
apt-key export 22F3D138 | gpg --dearmour -o /usr/share/keyrings/debian-buster-updates.gpg
apt-key export E562B32A | gpg --dearmour -o /usr/share/keyrings/debian-security-buster.gpg
cat > /etc/apt/preferences.d/chromium.pref << 'EOF'

Package: *
Pin: release a=eoan
Pin-Priority: 500

Package: *
Pin: origin "deb.debian.org"
Pin-Priority: 300

Package: chromium*
Pin: origin "deb.debian.org"
Pin-Priority: 700
EOF

apt-get update
apt-get install chromium chromium-driver

# Install Selenium
pip install selenium
```
