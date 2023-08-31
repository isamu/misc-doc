#### 機能として未利用
  about (string, optional): About the manifest (URL, email, github id, or twitter id)

#### model関連
  model (string, optional): LLM model (such as "gpt-4-613", the default is "gpt-3-turbo")
  temperature (string, optional): Temperature (the default is 0.7)

#### cli表示関連
 title (string, required): Title for the user to see
 bot (string, optional): Agent name
 you (string, optional): User name. The default is You({agent_name}).

#### Sample
sample (string, optional): Sample question (type "/sample" to send it)

#### cli表示＋アルファ
intro (array of strings, optional): Introduction statements (will be randomly selected)


#### prompt

prompt (array of strings, required): The system prompts which define the agent (required)

prompt ->
  {now} ->"%Y%m%dT%H%M%SZ"
  {random} -> listのデータをランダムに
  {resource} -> resourceのファイルの中身に差し替えられる

  list (array of string, optional): {random} will put one of them randamly into the prompt
  resource (string, optional): location of the resource file. Use {resource} to paste it into the prompt

#### query
  form (string): format string to extend user's query (e.g. "Write python code to {question}").
  functions (string, optional): location of the function definitions
    -> apiで投げるときに指定する

#### funcitonの戻り
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
