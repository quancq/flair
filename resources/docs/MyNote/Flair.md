a
=================

# 1. Kiểu dữ liệu cơ bản

* Token: chứa 1 từ
	* Truy cập text từ object Token: ``token.text``
	* Gán tag vào token: ``token.add_tag('ner', 'Loc')``
	* Truy cập tag ner và score tương ứng của token. Khi gán tag bằng hàm ``add_tag`` thì score = 1.0, còn khi predict thì sẽ có score của model
```python
	tag = token.get_tag('ner')
	print("Tag: {} - Score: {}".format(tag.value, tag.score))
```

* Sentence: chứa 1 câu văn bản, lưu 1 list các token
	* Khởi tạo câu với string đã được tách từ (các token cách nhau bởi space) hoặc chưa (nếu chưa thì thêm tham số ``use_tokenizer=True`` để flair dùng segtok tách từ)
	* Truy cập text của câu: ``sentence.to_original_text()``
	* Truy cập token đầu tiên của câu: ``sentence[0]``
	* Thêm một hoặc nhiều nhãn category cho câu: ``sentence.add_label("sports")``. Các nhãn này thuộc kiểu Label nên có score.

* Label: chứa nhãn (với từ có thể là ner, pos tag; với câu có thể là nhãn category phân loại)

* Span

# 2. Tagging

* Cách load pre trained model và gán nhãn cho các token trong câu
```python
from flair.models import SequenceTagger
tagger = SequenceTagger.load("ner")
sentence = Sentence("George Washington went to Washington .")
tagger.predict(sentence)
for token in sentence:
    tag = token.get_tag("ner")
    print("{} - {} - {}".format(token.text, tag.value, tag.score))
```

* Có các pre trained model được train trên các ngôn ngữ khác nhau, có model đa ngôn ngữ. Có model cho bài toán pos, sentiment.
