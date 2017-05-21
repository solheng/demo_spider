import requests
from bs4 import BeautifulSoup
import codecs
import os
url = 'http://finance.caixin.com/'
headers = {'User-Agent':'Mozilla/5.0 (Windows NT 10.0; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/57.0.2987.110 Safari/537.36'}
html = requests.get(url,headers=headers)
metadata = html.text
soup = BeautifulSoup(metadata,'html.parser')
news_links = soup.find_all('h4',limit=91)#class_='boxa'
print('新闻总数：{}'.format(len(news_links)))
fw = codecs.open('caixin_index.txt','a','utf-8')
urls = codecs.open('urls.txt','a','utf8')
lst = []
news_data_title = []
news_index = 1
for link in news_links:
    a = link.find('a')
    href = a.attrs['href']
    news_title = link.text
    news_data_title.append(news_title)
    lst.append(href)
    fw.write('新闻链接:{}'.format(href))
    fw.write('新闻标题:{}'.format (link.text + '\n'))
    urls.write(href)#写入href
#    print('新闻链接:{}'.format(href))
#    print('新闻标题:{}'.format(link.text + '\n'))
#print(lst)
for lll in lst:
    all_links = lll
    html = requests.get(all_links)
    metadata = html.text
    soup = BeautifulSoup(metadata,'html.parser')
    word = soup.find_all('p')
    print('标题：{}'.format(soup.h1.get_text()))
    wbdata = ''
    for w in word:
        wbdata += w.get_text()
    print(wbdata + '\n')
    root=r'D:\spider\caixin_news_menu'
    def write_txt(wbdata):
        f = codecs.open(os.path.join(root,str(news_index))+'.txt','w','utf-8')
        #f = codecs.open('all_news_text.txt','a','utf-8')
        f.write('标题：{}'.format(soup.h1.get_text()))
        f.write(wbdata)
        f.close()
    write_txt(wbdata)
    news_index += 1
    print(news_index)
#list写入TXT文件的问题(未完成)
#with open('urls.txt','a','utf8') as f:
#    for l in lst:
#        pickle.dump(l,f)








