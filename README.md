# test

# -*- coding: utf-8 -*-
# @Time    : 2018/7/25 0025 15:12
# @Author  : Zhaoti10222059
# @Site    : 
# @File    : word.py
# @Software: PyCharm

from docx import Document
from docx.shared import Inches
from docx import shape
from PIL import Image
from time import sleep
import os
import shutil
import zipfile
# document1 = Document('test.docx')
# doc_new = Document()
# #print type(document.paragraphs[2])
# print document1.get_picture()
# for text in  document1.paragraphs:
#     print text.text
#     print text,type(text)
#     doc_new.add_paragraph(text.text)
# doc_new.save('test1.doc')
#
# print

def get_image(dir,filename):
    #filename 是docx格式
    docname = filename.split(".")[0]
    shutil.copyfile(filename, docname + '.zip')
    f = zipfile.ZipFile("%s.ZIP" % docname, 'r')
    for file in f.namelist():
        if "word" in file:
            f.extract(file)  # 将压缩包里的word文件夹解压出来
    f.close()
    oldimagedir = r"%s\word\media" % dir  # 定义图片文件夹
    shutil.copytree(oldimagedir, "%s\%s" % (dir, docname))  # 拷贝到新目录，名称为word文件的名字
    os.remove(docname + '.zip')
    shutil.rmtree("%s\word" % dir)  # 删除word文件夹
    return str(dir) + '\\'+ str(docname) + '\\image1.png'


def handle_dir(dir):
    os.chdir(dir)
    dirlist = os.listdir(dir)
    for filename in dirlist:
        if filename.endswith(".docx"):
            #print get_image(dir,filename)
            doc_before = Document(filename)
            #doc_new = Document()
            title = doc_before.paragraphs[0].text
            author = doc_before.paragraphs[1].text
            image = get_image(dir,filename)
            print title,author,image
            for text in doc_before.paragraphs[3:]:
                print text.text
                #print text,type(text)
                #doc_new.add_paragraph(text.text)
                #doc_new.save('test1.doc')

            #shutil.copyfile(i, i.split(".")[0]+'.zip')



if __name__ == '__main__':
    handle_dir('D:\PycharmProjects\google_health')
    pass








from googletrans import Translator
translator = Translator()
#print translator.translate('今天天气不错').text
#print translator.translate('今天天气不错', dest='ja').text
#print translator.translate('今天天气不错', dest='ko').text

translations = translator.translate(['today is monday', 'today is tuesday', 'the lazy dog'], dest='zh-cn')
for translation in translations:
    print(translation.origin, ' -> ', translation.text)
