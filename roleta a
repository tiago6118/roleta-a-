import time
import tkinter as tk
from selenium import webdriver
from selenium.webdriver.common.by import By
from threading import Thread

url = "https://www.playpix.com/pb/live-casino/home/-1/All?openGames=40003094-real&gameNames=Roulette%20A"

driver = webdriver.Chrome()
driver.get(url)
janela = driver.window_handles[0]
resultado = None
check_resultado = None

def extracao():
    global resultado
    resultado = []
    driver.switch_to.window(janela)
    while len(driver.find_elements(By.XPATH, '/html/body/div[1]/div[3]/div[1]/div[1]/div/iframe')) == 0:
        time.sleep(2)
    iframe1 = driver.find_element(By.XPATH, '/html/body/div[1]/div[3]/div[1]/div[1]/div/iframe')
    driver.switch_to.frame(iframe1)
    while len(driver.find_elements(By.XPATH, '/html/body/div[2]/div/div[1]/div/iframe')) == 0:
        time.sleep(2)
    iframe2 = driver.find_element(By.XPATH, '/html/body/div[2]/div/div[1]/div/iframe')
    driver.switch_to.frame(iframe2)
    while len(driver.find_elements(By.XPATH, '/html/body/div[2]/div/div[1]/div[8]/div[3]/div/div[1]')) == 0:
        time.sleep(2)
    resultado = driver.find_element(By.XPATH, '/html/body/div[2]/div/div[1]/div[8]/div[3]/div/div[1]').text.split()
    return resultado

def atualizar_tela():
    global check_resultado
    while True:
        extracao()
        if resultado != check_resultado:
            check_resultado = resultado
            resultado_label.config(text=" ".join(resultado))
        time.sleep(2)

root = tk.Tk()
root.title("Resultados do Jogo")
resultado_label = tk.Label(root, text="", font=("Helvetica", 16))
resultado_label.pack(pady=20)
thread = Thread(target=atualizar_tela)
thread.daemon = True
thread.start()
root.mainloop()
