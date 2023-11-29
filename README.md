

# カウントダウンリピーターのアプリ

# 必要なモジュールをインポートする
import time
import tkinter as tk
import pyttsx3

# 音声エンジンを初期化する
engine = pyttsx3.init()

# カウントダウンの秒数を設定する
seconds = [10, 5, 3]

# カウントダウンの関数を定義する
def countdown(sec):
    # 音声でカウントダウンを開始する
    engine.say(f"{sec}秒のカウントダウンを開始します")
    engine.runAndWait()
    # 秒数を表示する
    label.config(text=sec)
    # 1秒待つ
    time.sleep(1)
    # 秒数を減らす
    sec -= 1
    # 秒数が0になるまで繰り返す
    while sec > 0:
        # 秒数を音声で出力する
        engine.say(str(sec))
        engine.runAndWait()
        # 秒数を表示する
        label.config(text=sec)
        # 1秒待つ
        time.sleep(1)
        # 秒数を減らす
        sec -= 1
    # 音声でカウントダウンが終了したことを伝える
    engine.say("カウントダウンが終了しました")
    engine.runAndWait()
    # 秒数を表示する
    label.config(text=sec)

# 繰り返しの関数を定義する
def repeat():
    # スタートボタンを無効にする
    start_button.config(state=tk.DISABLED)
    # ストップボタンを有効にする
    stop_button.config(state=tk.NORMAL)
    # グローバル変数を宣言する
    global running
    # 繰り返しを開始する
    running = True
    # 選択された秒数を取得する
    sec = var.get()
    # 繰り返しを止めるまでカウントダウンを実行する
    while running:
        countdown(sec)

# ストップの関数を定義する
def stop():
    # スタートボタンを有効にする
    start_button.config(state=tk.NORMAL)
    # ストップボタンを無効にする
    stop_button.config(state=tk.DISABLED)
    # グローバル変数を宣言する
    global running
    # 繰り返しを停止する
    running = False

# ウィンドウを作成する
window = tk.Tk()
window.title("カウントダウンリピーター")
window.geometry("300x200")

# ラベルを作成する
label = tk.Label(window, text="カウントダウンリピーター", font=("Arial", 20))
label.pack()

# ラジオボタンを作成する
var = tk.IntVar()
var.set(10)
radio_button_10 = tk.Radiobutton(window, text="10秒", variable=var, value=10)
radio_button_10.pack()
radio_button_5 = tk.Radiobutton(window, text="5秒", variable=var, value=5)
radio_button_5.pack()
radio_button_3 = tk.Radiobutton(window, text="3秒", variable=var, value=3)
radio_button_3.pack()

# スタートボタンを作成する
start_button = tk.Button(window, text="スタート", command=repeat)
start_button.pack()

# ストップボタンを作成する
stop_button = tk.Button(window, text="ストップ", command=stop, state=tk.DISABLED)
stop_button.pack()

# ウィンドウを表示する
window.mainloop()
