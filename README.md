# Naver_Stock_Crawl
Naver Stock News Web Crawler

## 1. 파일 경로
Colab Notebooks폴더에 crawl_data와 crawled_data 폴더를 추가함.

- crawl_data: company_list.txt 저장
- crawled_data: 최종 CSV 저장

## 2. 웹 크롤러
참고2: https://hengju.tistory.com/36  ***


헹쥬 블로그 코드를 참고했는데 Dataframe을 만드는 과정에서 오류가 있었다.\n
위 링크를 통해 이렇게 해결하고 파일에 내용을 덧붙일 수 있도록 mode='a'로 변경했다.
```
df_result.to_csv('./crawled_data/'+'page' + str(page) + '.csv', mode='a', encoding='utf-8-sig')
```

\n\n
헹쥬 블로그 코드에서는 뉴스 본문을 가져올 수 없어서 아래 코드를 추가했다.
```
# 뉴스 본문
        links = html.select('.title') 

        content_result =[]
        for link2 in links: 
          add2 = 'https://finance.naver.com' + link2.find('a')['href']
          url2 = add2
          print("url2: "+ url2)
          source_code2 = requests.get(url2).text
          html2 = BeautifulSoup(source_code2, "lxml")

          contents = html2.select('.scr01')
          content_whole = [content.get_text() for content in contents] 
          content_result.append(content_whole)



# 이건 수정한 부분! 최종 첨부내용에 뉴스본문 추가
result= {"날짜" : date_result, "언론사" : source_result, "기사제목" : title_result, "링크" : link_result, "본문" : content_result}
```
