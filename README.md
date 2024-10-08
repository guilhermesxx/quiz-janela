import tkinter as tk
import winsound

class QuizTheWalkingDead:
    def __init__(self, root):
        self.root = root
        self.root.title("Quiz The Walking Dead")
        self.root.geometry("400x300")
        self.root.configure(bg="lightblue")

        self.perguntas = [
            {
                "pergunta": "Quem é o protagonista da série 'The Walking Dead'?",
                "opcoes": ["Rick Grimes", "Daryl Dixon", "Glenn Rhee"],
                "resposta": "Rick Grimes"
            },
            {
                "pergunta": "Qual é a capital do grupo de sobreviventes liderado por Rick?",
                "opcoes": ["Atlanta", "Alexandria", "Hilltop"],
                "resposta": "Alexandria"
            },
            {
                "pergunta": "Qual personagem usa um arco e flecha?",
                "opcoes": ["Rick Grimes", "Daryl Dixon", "Carl Grimes"],
                "resposta": "Daryl Dixon"
            },
            {
                "pergunta": "Quem é o melhor amigo de Rick Grimes?",
                "opcoes": ["Shane Walsh", "Glenn Rhee", "Daryl Dixon"],
                "resposta": "Shane Walsh"
            },
            {
                "pergunta": "Qual é o nome da filha de Rick Grimes?",
                "opcoes": ["Judith", "Sophia", "Maggie"],
                "resposta": "Judith"
            },
            {
                "pergunta": "Qual é o nome do vilão que usa uma Lucille?",
                "opcoes": ["Negan", "The Governor", "Alpha"],
                "resposta": "Negan"
            },
            {
                "pergunta": "Qual grupo é conhecido por usar máscaras de zumbis?",
                "opcoes": ["Os Sussurradores", "Os Salvadores", "Os Vivos"],
                "resposta": "Os Sussurradores"
            },
            {
                "pergunta": "Quem se sacrifica para salvar o grupo na temporada 4?",
                "opcoes": ["Hershel", "Beth", "Tara"],
                "resposta": "Hershel"
            },
            {
                "pergunta": "Qual é o nome da mulher que era médica no grupo?",
                "opcoes": ["Carol", "Tara", "Samantha"],
                "resposta": "Carol"
            },
            {
                "pergunta": "Qual é o nome da série derivada de 'The Walking Dead'?",
                "opcoes": ["Fear the Walking Dead", "World Beyond", "The Walking Dead: Beyond"],
                "resposta": "Fear the Walking Dead"
            }
        ]

        self.pergunta_atual = 0
        self.resposta_label = tk.Label(root, text="", bg="lightblue")
        self.resposta_label.pack()

        self.pergunta_label = tk.Label(root, text="", bg="lightblue")
        self.pergunta_label.pack(pady=10)

        self.var = tk.StringVar(value="")
        self.opcoes = []

        for _ in range(3):
            op = tk.Radiobutton(root, text="", variable=self.var, value="", bg="lightblue")
            op.pack(anchor="w")
            self.opcoes.append(op)

        self.botao_enviar = tk.Button(root, text="Enviar Resposta", command=self.enviar_resposta)
        self.botao_enviar.pack(pady=10)

        self.mostrar_pergunta()

    def mostrar_pergunta(self):
        pergunta = self.perguntas[self.pergunta_atual]
        self.pergunta_label.config(text=pergunta["pergunta"])
        for i, opcao in enumerate(pergunta["opcoes"]):
            self.opcoes[i].config(text=opcao, value=opcao)
        self.resposta_label.config(text="")

    def enviar_resposta(self):
        if self.var.get() == self.perguntas[self.pergunta_atual]["resposta"]:
            self.resposta_label.config(text="Você acertou!", fg='green')
            winsound.Beep(1000, 500)
        else:
            self.resposta_label.config(text="Você errou!", fg='red')
        
        self.pergunta_atual += 1
        if self.pergunta_atual < len(self.perguntas):
            self.root.after(1000, self.mostrar_pergunta)
        else:
            self.mostrar_resultado()

    def mostrar_resultado(self):
        self.pergunta_label.config(text="Quiz Finalizado!")
        self.var.set("")
        for op in self.opcoes:
            op.pack_forget() 

        self.resposta_label.config(text="Obrigado por jogar!")

root = tk.Tk()
app = QuizTheWalkingDead(root)
root.mainloop()
