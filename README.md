# Translator1_App
import tkinter as tk
from tkinter import ttk
from libretranslatepy import LibreTranslateAPI
from PIL import Image, ImageTk
from urllib.request import urlopen
import io

# ico_url = r"https://www.freepnglogos.com/uploads/translate-logo-png/logos-translate-icon-for-website-10.png"
# image_url = r"https://static.wikia.nocookie.net/logopedia/images…/latest/scale-to-width-down/200?cb=20200929192029"

lt = LibreTranslateAPI("https://translate.argosopentech.com/")
langs = lt.languages()
lang_name = [lang["name"] for lang in langs]
lang_code = {lang["name"]:lang["code"] for lang in langs}


# initialize the window
win = tk.Tk()
win.geometry("600x500")
win.title("Translator App")
win.config(bg="#040c36")
win.resizable(False, False)

# imgs
img = tk.PhotoImage(file=r"C:\Users\User\tk\tr.png")
win.iconphoto(False, img)

image = tk.PhotoImage(file=r"C:\Users\User\tk\images.png").subsample(2)
tr_img = tk.Label(win, image=image, padx=5, pady=5)
tr_img.place(relx=0.495, rely=0.18, anchor='center')

# input side
input_lab = tk.Label(win, text="Input Language", font="arial 13 bold")
input_lab.place(x= 68, y= 45)
input_lan = ttk.Combobox(win, width=15, values=lang_name)
input_lan.place(x=75, y= 90)
input_lan.set("Input Language")
input_txt = tk.Text(win, bg="white", font="arial 14", width=18, height=10)
input_txt.place(x=30, y=130)


# output side
output_lab = tk.Label(win, text="Output Language", font="arial 13 bold")
output_lab.place(x= 400, y= 45)
output_lan = ttk.Combobox(win, width=15, values=lang_name)
output_lan.place(x=407, y= 90)
output_lan.set("Translated Language")
output_txt = tk.Text(win, bg="white", font="arial 14", width=18, height=10)
output_txt.place(x=362, y=130)

# buttons
def translate():
    try:
        tran = lt.translate(input_txt.get("1.0", tk.END), lang_code[input_lan.get()], lang_code[output_lan.get()])
        output_txt.insert("1.0", tran)
    except:
        output_txt.insert("1.0", "There Is Something Wrong")


trans_btn = tk.Button(win, text="Translate", bg="#005a5e", padx=5, command=translate)
trans_btn.place(x=265, y=200)

def clear():
    try:
        input_txt.delete("1.0", tk.END)
        output_txt.delete("1.0", tk.END)
    except:
        output_txt.insert("1.0", "There Is Something Wrong")

cls_btn = tk.Button(win, text="Clear",bg="#db3939", padx=5, command=clear )
cls_btn.place(x=275, y=240)

# 
cp = tk.Label(win, text="All Copyrights © Reserved For Ali Elbareg", font="arial 15 bold", padx=5, pady=5)
cp.place(relx=0.168, rely=0.8)

win.mainloop()

