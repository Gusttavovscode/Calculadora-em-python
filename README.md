import tkinter as tk

# Função para atualizar a entrada
def clicar_botao(valor):
    entrada.insert(tk.END, valor)

# Função para limpar a entrada
def limpar():
    entrada.delete(0, tk.END)

# Função para avaliar a expressão matemática
def calcular():
    try:
        resultado = eval(entrada.get())
        entrada.delete(0, tk.END)
        entrada.insert(tk.END, str(resultado))
    except Exception as e:
        entrada.delete(0, tk.END)
        entrada.insert(tk.END, "Erro")

# Configuração da janela principal
janela = tk.Tk()
janela.title("Calculadora")
janela.geometry("300x400")

# Campo de entrada
entrada = tk.Entry(janela, font=("Arial", 24), borderwidth=2, relief="solid", justify="right")
entrada.grid(row=0, column=0, columnspan=4, ipadx=8, ipady=8, pady=10)

# Botões
botoes = [
    ('7', 1, 0), ('8', 1, 1), ('9', 1, 2), ('/', 1, 3),
    ('4', 2, 0), ('5', 2, 1), ('6', 2, 2), ('*', 2, 3),
    ('1', 3, 0), ('2', 3, 1), ('3', 3, 2), ('-', 3, 3),
    ('C', 4, 0), ('0', 4, 1), ('=', 4, 2), ('+', 4, 3)
]

for (texto, linha, coluna) in botoes:
    if texto == 'C':
        comando = limpar
    elif texto == '=':
        comando = calcular
    else:
        comando = lambda t=texto: clicar_botao(t)

    tk.Button(janela, text=texto, font=("Arial", 18), command=comando, width=5, height=2).grid(row=linha, column=coluna, padx=5, pady=5)

# Inicia o loop principal da interface
janela.mainloop()
