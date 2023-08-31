## manifest file
#### 機能として未利用
- about (string, optional): About the manifest (URL, email, github id, or twitter id)
  - manifestファイルの説明

#### model関連
manifestファイルごとに利用するLLMモデルを指定

- model (string, optional): LLM model (such as "gpt-4-613", the default is "gpt-3-turbo")
  - そのmanifestで使うモデルを指定する
- temperature (string, optional): Temperature (the default is 0.7)
  - modelに渡すtemperature

#### cli表示関連
SlashGPTのCLI動作時に、CLIの出力として使われる設定（LLM・GPTの動作に影響なし）

- title (string, required): Title for the user to see
  - Agent起動時（切替時）に表示される
```
Activating: Main Dispatcher
```
- bot (string, optional): Agent name
   - LLMからの応答時に表示される名前
```
botname: Hello, I am bot.
```
- you (string, optional): User name. The default is You({agent_name}).
  - 入力のプロンプトや、functionの動作後、再度ユーザの入力を問い合わせる時などに表示される
```
You(simple)
```

#### Sample

LLMの動作検証やユーザへの例として、サンプルクエリを設定（LLM・GPTの動作に影響なし）

- sample (string, optional): Sample question (type "/sample" to send it)
  - 事前の用意するpromptへの問い合わせの内容を記述する
  - prefixがsampleで始まるkeyは、全てsampleとして実行可能
    - sample_1に記述すれば /sample_1 で利用可能

#### CLI表示 ＋ システムプロンプト

- intro (array of strings, optional): Introduction statements (will be randomly selected)
   - Agent起動時（切替時）に表示され、promptにも渡されるシステムメッセージ

#### prompt
システムメッセージとしてLLM/GPTに渡すシステムプロンプト。

- prompt (array of strings, required): The system prompts which define the agent (required)
  - LLMに渡すシステムプロンプトの文
    - 以下のtemplate記法は、置換される
      - {now}
        - "%Y%m%dT%H%M%SZ" 形式の日付
      - {resource}
        - 後述するresource要素のファイルの中身に差し替えられる
      -  {random}
        - list内のデータをランダムに置換する
- list (array of string, optional): {random} will put one of them randamly into the prompt
- resource (string, optional): location of the resource file. Use {resource} to paste it into the prompt

#### query
ユーザの入力をLLM/GPTにわたすときに、ユーザのメッセージ/クエリーを加工したり、funcitonsの設定をする
  
- form (string): format string to extend user's query (e.g. "Write python code to {question}").
   - LLMに渡すメッセージ。{question}部分がユーザの入力となるため、入力をラップして渡すことができる
- functions (string, optional): location of the function definitions
   - functionsの設定

#### funcitonの戻り
LLM/GPTからfunctionの結果が戻ってきた場合の動作を指定する。

  actions (object, optional): Template-based function processor (see details below)
    -> 分岐。
     - rest
     - graph
     - template
  Pythonのコードを実行する
    notebook (boolean): create a new notebook at the beginning of each session (for jupyter2)
       - 実行する 
    module (string, optional): location of the Python script to be loaded for function calls
      - codeを実行する
    共通
      result_form (string): format string to extend function call result.
        jupyterを参照   

skip_function_result (boolean): skip the chat completion right after the function call.




embeddings
  embeddings (object, optional):
  name (string, optional): index name of the embedding vector database
