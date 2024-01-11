# 「昭和・平成書き言葉コーパス」統計情報

## ファイル
 - [shc-data/](https://drive.google.com/drive/folders/16LuPxgOF8jtt3KbiksQpmYiFpxCJ2jiy)
   - [ngram\_word2vec](https://drive.usercontent.google.com/download?id=1FvaSSiuC9YSa8p-sB9nv88i0_3GXpc75)：NLP2024の原稿（4.1節）で使用した単語分散表現の学習結果。
   - [svmlight\_ngram](https://drive.usercontent.google.com/download?id=1x6TDP8BosoVqwKbcN2l-INbXxe1FD_Ca)：加工した統計情報。
 - （参考）[chj-shc\_svmlight\_ngram](https://bit.ly/3HT96Ii)：近現代雑誌コーパス（CHJ雑誌・SHC雑誌）を加工した統計情報。2022年時点のもの。

## 説明 
「昭和・平成書き言葉コーパス」の統計情報を`ngram`・`svmlight`形式で加工。  
雑誌（`magazine`）、書籍（`bestseller`）、新聞（`newspaper`）に分けて公開。
 - `ngram`：単語 / 語彙素ID の 1~5 gram とその頻度を `tab` 区切りで出力
```
# 単語 5-gram （surface_ngram/magazine/magazine_1933-1933_5gram.txt）
た の で ある 。  1697
の で あつ た 。	639

# 語彙素ID 5-gram （lemmaID_ngram/magazine/magazine_1933-1933_5gram.txt）
21642 28990 22916 1216 25    1820
86345 86345 86345 86345 86345    921
```
 - `svmlight`：語彙素ID に関する共起情報（`共起する語彙素ID:共起回数` 形式、20回以上出現する語彙素ID、前後4単語）を `tab` 区切りで出力
```
# 語彙素ID svmlight （lemmaID_svmlight/magazine/magazine_1933-1933_threshold-20_svmlight.txt）
0	0:1340 1:243 4:19 5:20 6:8 ...
```

また、単語5-gramで学習した単語分散表現（Word2Vec, Skip-Gram with Negative Sampling）も公開。
 - 昭和（1933年〜1989年）
   - `showa_all.model`：すべての分野を結合して学習
   - `showa_bestseller.model`：書籍のみを使用して学習
   - `showa_magazine.model`：雑誌のみを使用して学習
   - `showa_newspaper.model`：新聞のみを使用して学習
 - 平成（1989年〜2013年）
   - `heisei_all.model`：すべての分野を結合して学習
   - `heisei_bestseller.model`：書籍のみを使用して学習
   - `heisei_magazine.model`：雑誌のみを使用して学習
   - `heisei_newspaper.model`：新聞のみを使用して学習
```
from gensim.models import Word2Vec

w2v = Word2Vec.load("heisei_all.model")
w2v.wv.most_similar("通信")
# Output
[('化学', 0.7626633048057556), ('印刷', 0.7593160271644592), 
 ('航空', 0.7480340003967285), ('製薬', 0.7324012517929077), 
 ('メディア', 0.7320590615272522), ('系列', 0.7316423654556274), 
 ('流通', 0.7178449630737305), ('新華', 0.7121592164039612), 
 ('住友', 0.7060260772705078), ('各社', 0.7044658660888672)]
```

## 参照
> 近藤 明日子, 相田 太一, 小木曽 智信. 近現代雑誌通時コーパスの語彙統計情報の公開. 言語処理学会第28回年次大会 (NLP2022), pp.1695-1698. https://www.anlp.jp/proceedings/annual_meeting/2022/pdf_dir/PT4-1.pdf  
> 相田 太一, 近藤 明日子, 小木曽 智信. 「昭和・平成書き言葉コーパス」の語彙統計情報の公開. 言語処理学会第30回年次大会 (NLP2024).  
> 小木曽 智信, 近藤 明日子, 髙橋 雄太, 間淵 洋子.「『昭和・平成書き言葉コーパス』の設計・構築・公開」『情報処理学会誌』65(2). https://clrd.ninjal.ac.jp/shc/doc/IPSJ_SHC_preprint.pdf
