from chatterbot import ChatBot
from chatterbot.trainers import ListTrainer
import json

# Criação do chatbot
faq_bot = ChatBot("FAQ_ENEM", read_only=True)

# Treinamento com base de conhecimento
trainer = ListTrainer(faq_bot)

# Carrega os pares de perguntas e respostas
with open("base_conhecimento.json", "r", encoding="utf-8") as f:
    conhecimento = json.load(f)

trainer.train(conhecimento)

print("Chatbot FAQ ENEM em português (digite 'sair' para encerrar)")
while True:
    pergunta = input("Você: ")
    if pergunta.lower() == "sair":
        print("Bot: Até mais!")
        break
    resposta = faq_bot.get_response(pergunta)
    print(f"Bot: {resposta}")

