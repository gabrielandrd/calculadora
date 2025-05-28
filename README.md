# calculadora
calculadora simples e visual
import ipywidgets as widgets
from IPython.display import display

# Funções matemáticas
def somar(a, b): return a + b
def subtrair(a, b): return a - b
def multiplicar(a, b): return a * b
def dividir(a, b): return a / b if b != 0 else "Erro: divisão por zero"


def formatar_resultado(valor):
    if isinstance(valor, (int, float)) and valor == int(valor):
        return str(int(valor))  # Ex: 10.0 → 10
    return str(valor)


num1 = widgets.FloatText(description='Número 1:', style={'description_width': '80px'})
num2 = widgets.FloatText(description='Número 2:', style={'description_width': '80px'})
operacao = widgets.Dropdown(
    options=[('Soma', 'soma'), ('Subtração', 'subtracao'), ('Multiplicação', 'multiplicacao'), ('Divisão', 'divisao')],
    description='Operação:',
    style={'description_width': '80px'}
)
botao = widgets.Button(description='Calcular', button_style='success')
resultado_box = widgets.HTML(
    value="<div style='font-size:18px; color:#333; padding:10px; border:2px solid #ccc; border-radius:8px; background:#f9f9f9; width:300px;'>Resultado: </div>"
)


def ao_clicar(botao):
    a = num1.value
    b = num2.value
    op = operacao.value

    if op == 'soma':
        resultado = somar(a, b)
    elif op == 'subtracao':
        resultado = subtrair(a, b)
    elif op == 'multiplicacao':
        resultado = multiplicar(a, b)
    elif op == 'divisao':
        resultado = dividir(a, b)

    resultado_formatado = formatar_resultado(resultado)

    resultado_box.value = f"""
    <div style='font-size:18px; color:#222; padding:10px; border:2px solid #ccc; border-radius:8px; background:#e8f5e9; width:300px;'>
        <b>Resultado:</b> {resultado_formatado}
    </div>
    """

botao.on_click(ao_clicar)

display(num1, num2, operacao, botao, resultado_box)

