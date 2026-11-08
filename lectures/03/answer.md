# 第3回 解答

## 演習

- 第1回（素のLLM）とエージェントの回答の違い：用語集に忠実に回答してくれる。回答が簡潔で余計なことは答えない。
- `--trace` で見えたツール呼び出し（ツール名と引数）：serch_glossary 'LoRA','QLoRA'
- 1つの質問での LLM 呼び出し回数（`requests`）：2回
- 追加したツールと、docstring に書いた説明：make_quiz
"""指定した回の用語から1つを選び、確認問題と答えを返す。
「第3回の確認問題を出して」のように、復習用の問題を求められた時に使う。
"""

## 宿題

- 取り組んだレベル：基礎 /　
- やったこと：
　　①基礎：app/tool.py のうち、search_glossary のdocstring の「用語を1つだけ入れる」を「まとめて入れる」に変えた後、「LoRAとQLoRAの違い」を質問した。
　　②基礎：app/agent.py のうち、「回答の最後に、関係する回（第N回）を示す」を削った。
　　③基礎：app/agent.py のうち、「必ず用語集を確認する」の行を消して質問した。
- 結果：
　　①　最初の設定では、単語を1つずつ検索していた。
[tool call]   search_glossary({'query': 'LoRA'})
[tool call]   search_glossary({'query': 'QLoRA'})
　　　　「用語をまとめて入れる」に変えた後は、LoRA とQLoRA をまとめて検索していた。
[tool call]   search_glossary({'query': 'LoRA QLoRA'})
　　　　最も、検索結果は、LoRA やlecture 2 が返ってきており、LLMの回答は誤っていなかった。
　　② 「回答の最後に、関係する回（第N回）を示す」を削ると、「関係する回」の出力は無くなった。
　　③ 「必ず用語集を確認する」の行を消しても、tool call がされた。

- 気づき・疑問：
クエリの入力方法や、「関係する回の明示」などについては、差異が出たが、「必ず用語集を確認する」の行を消しても挙動に差が生じなかった。なぜだろう。INSTRUCTION に指示がなくても、tool の存在が書かれているので、そこを見て呼び出しているのだろうか？（→search_glossary の行自体を削除すると、tool call しない。他方で、INSTRUCTIONS を丸ごと削除しても、依然としてtool call される。
