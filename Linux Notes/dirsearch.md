Dirsearch  tool is an advanced [[Linux]] command-line tool designed to brute-force directories and files in web servers or web path scanners. As Dirsearch is an advanced tool, it allows hackers to perform a complex web directories discovery,  with a customized wordlist. It's preinstalled in Kali Linux distro.

***Installation
```
git clone https://github.com/maurosoria/dirsearch.git
```
Make sure you run the requirement file
```
pip3 install -r requirements.txt
```
Type this command for help
```
python3 dirsearch.py --help
```
Simple Usage
```
python3 dirsearch.py -u https://example.com
```
Exclude some extension
```
python3 dirsearch.py -e php,html,js -u https://example.com
```
Using wordlist
```
python3 dirsearch.py -e php,html,js -u https://example.com -w /usr/share/wordlists/dirb/common.txt
```

For more Option
https://www.geeksforgeeks.org/how-to-find-hidden-web-directories-with-dirsearch/