# POO-game
# I made an RPG game in my intermediate Python minicourse using Object Oriented Programming.


import random #importar números aleatórios para vida, ataque e defesa dos personagens.

class Item:#Classe item que os jogadores podem conseguir durante o jogo
   def __init__(self, nome, tipo, poder):
       self.nome = nome
       self.tipo = tipo
       self.poder = poder

   # mostrar informações do item
   def info(self):
       print(f"Item: {self.nome}  Tipo: {self.tipo}  Poder: {self.poder}")

class SerVivo:#Classe que todos os seres vivos do jogo irão herdar.
   def __init__(self, nome, vida, ataque, defesa):
       self.nome = nome
       self.vida = vida
       self.ataque = ataque
       self.defesa = defesa

   def info(self):#Para mostrar as informações dos seres vivos
       print(f"Nome: {self.nome}")
       print(f"Vida: {self.vida}  Ataque: {self.ataque}  Defesa: {self.defesa}")

class Personagem(SerVivo): #Criação dos personagens principais herdando de seres vivos
   def __init__(self, nome, raca, classe, vida, ataque, defesa):
       super().__init__(nome, vida, ataque, defesa) #1 exemplo de herança dentre vários no código.
       self.raca = raca
       self.classe = classe
       self.inventario = []

   def info(self): #Para mostrar as informações dos itens
       super().info()
       print(f"Raça: {self.raca}  Classe: {self.classe}")
       print("Inventário:")
       for item in self.inventario:
           item.mostrar_info()
#Exemplo de composição
   def adicionar_item(self, item):
       self.inventario.append(item)

class Inimigo(SerVivo):#Classe inimigo, não coloquei nada pois ele só precisa das coisas que ja tem na classe SerVivo
   pass

class NPC(SerVivo):#Classe NPC
   def __init__(self, nome, papel, vida, ataque, defesa):
       super().__init__(nome, vida, ataque, defesa)
       self.papel = papel

   def info(self):#Mostrar as informações
       super().info()
       print(f"Papel: {self.papel}")

class Equipe:#Criei uma classe equipe para cada vez que um personagem seja criado ele se direcione para a sua determinada equipe
   def __init__(self):
       self.membros = []

   def adicionar_membro(self, membro):
       self.membros.append(membro)

   def info(self):
       for membro in self.membros:
           membro.info()


class Mundo:
   # Classe para criar os personagens
   def __init__(self):
       self.equipe_personagens = Equipe()
       self.equipe_inimigos = Equipe()
       self.equipe_npcs = Equipe()

   def criar_personagem(self):
       nome = input("Digite o nome do personagem: ")

       # Escolher a raça do personagem
       print("Escolha a raça do personagem:")
       print("1. Humano")
       print("2. Ogro")
       print("3. Elfo")

       raca_escolhida = int(input())
       if raca_escolhida == 1:
           raca = "humano"
       elif raca_escolhida == 2:
           raca = "ogro"
       elif raca_escolhida == 3:
           raca = "elfo"
       else:
           print("Opção inválida. Escolhendo raça aleatória.")


       # Escolher as classes do personagem
       print("Escolha a classe do personagem:")
       print("1. Mago")
       print("2. Paladino")
       print("3. Feiticeiro")

       classe_escolhida = int(input())
       if classe_escolhida == 1:
           classe = "mago"
       elif classe_escolhida == 2:
           classe = "paladino"
       elif classe_escolhida == 3:
           classe = "feiticeiro"
       else:
           print("Opção inválida. Escolhendo classe aleatória.")

# Esacolha aleatória da quantidade de vida, ataque e defesa.
       vida = random.randint(50, 100)
       ataque = random.randint(10, 20)
       defesa = random.randint(5, 15)

       novo_personagem = Personagem(nome, raca, classe, vida, ataque, defesa)
       self.equipe_personagens.adicionar_membro(novo_personagem)
       print("Personagem criado com sucesso!")

   def criar_inimigo(self): #Criar inimigo
       nome = input("Digite o nome do inimigo: ")
       vida = random.randint(30, 70)
       ataque = random.randint(5, 15)
       defesa = random.randint(3, 10)

       novo_inimigo = Inimigo(nome, vida, ataque, defesa)
       self.equipe_inimigos.adicionar_membro(novo_inimigo)
       print("Inimigo criado com sucesso!")

   def criar_npc(self): #Criar Npc
       nome = input("Digite o nome do NPC: ")
       papel = input("Digite o papel do NPC: ")
       vida = random.randint(30, 70)
       ataque = random.randint(5, 15)
       defesa = random.randint(3, 10)

       novo_npc = NPC(nome, papel, vida, ataque, defesa)
       self.equipe_npcs.adicionar_membro(novo_npc)
       print("NPC criado com sucesso!")

   def menu_principal(self): #Menu de opçõespara o jogador escolher o que fazer
       while True:
           print("   MENU PRINCIPAL ")
           print("1. Criar Personagem")
           print("2. Criar Inimigo")
           print("3. Criar NPC")
           print("4. Listar Personagens")
           print("5. Listar Inimigos")
           print("6. Listar NPCs")
           print("0. Sair")

           escolha = input("Escolha uma opção: ")

           if escolha == '1':
               self.criar_personagem()
           elif escolha == '2':
               self.criar_inimigo()
           elif escolha == '3':
               self.criar_npc()
           elif escolha == '4':
               print("   PERSONAGENS ")
               self.equipe_personagens.info()
           elif escolha == '5':
               print("   INIMIGOS ")
               self.equipe_inimigos.info()
           elif escolha == '6':
               print("    NPCs ")
               self.equipe_npcs.info()
           elif escolha == '0':
               print("Saindo do jogo!")
               break
           else:
               print("Opção inválida. Tente novamente.")

if __name__ == "__main__":
   jogo = Mundo()
   jogo.menu_principal()


