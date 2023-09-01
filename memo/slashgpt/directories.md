 
- lib - SlashGPTのプログラム一式
- manifests - マニフェストファイル一式
- config - llmの設定ファイル
- resources
  - functionsの要素として読み込まれる
    - llmにfunctionsとして渡される 
  - resouceパラメータで読み込まれて、プロンプトに展開される
  - moduleでほげほげ？？
- data - functionsから利用するデータ
- notebooks - notebooks = true時に読み込まれるipynb
- output - ログなどの出力先
- plugins - pluginで利用するLLM engine
- samples - SimpleGPT.pyやAgentGPT.pyなどのlib以下のmoduleを使ったサンプルプログラム
- test - autotestの設定ファイル
- tests - unit test