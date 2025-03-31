# Lógica Fuzzy e Aplicação em Inteligência Artificial

Este repositório contém uma revisão bibliográfica sobre **Lógica Fuzzy** e uma demonstração de como essa técnica pode ser aplicada para resolver um problema de **Controle de Temperatura** em um sistema de climatização inteligente. O exemplo prático é implementado em Python usando a biblioteca `scikit-fuzzy`, que facilita a criação de sistemas de lógica fuzzy.

## 1. Introdução à Lógica Fuzzy

A **Lógica Fuzzy** (ou Lógica Difusa) é uma extensão da lógica booleana clássica, onde os valores não são restritos a apenas "verdadeiro" ou "falso" (1 ou 0), mas sim podem assumir qualquer valor entre 0 e 1. Isso permite representar incertezas e imprecisões de maneira mais próxima da forma como os seres humanos pensam e tomam decisões.

### Características principais:
- **Conjuntos Fuzzy**: Elementos podem ter um grau de pertencimento entre 0 e 1, permitindo um comportamento mais flexível do que os conjuntos clássicos.
- **Operadores Fuzzy**: Analogamente aos operadores da lógica clássica (como AND, OR e NOT), mas com valores contínuos.
- **Inferência Fuzzy**: Processo de dedução baseado em regras fuzzy, permitindo chegar a conclusões a partir de várias informações imprecisas.

## 2. Aplicações da Lógica Fuzzy em Inteligência Artificial

A lógica fuzzy é amplamente utilizada para modelar sistemas com imprecisões, como **controle de processos**, **análise de dados**, **diagnóstico médico**, entre outros. Ela permite criar sistemas mais robustos para lidar com variáveis que não podem ser precisamente medidas.

### Exemplos de Aplicação:
- **Sistemas de Controle**: Como o controle de temperatura de um forno ou sistema de climatização.
- **Análise de Riscos**: Avaliar riscos e probabilidades em sistemas financeiros ou de segurança.
- **Sistemas de Diagnóstico**: Diagnóstico médico baseado em sintomas imprecisos.

## 3. Problema de Inteligência Artificial Resolvido com Lógica Fuzzy

### Problema: Controle de Temperatura de um Sistema de Climatização Inteligente

O controle de temperatura em um ambiente é um problema comum que pode ser resolvido de forma eficiente utilizando a lógica fuzzy. Nesse exemplo, o sistema ajusta a intensidade do ar-condicionado ou aquecedor com base na temperatura ambiente, mantendo o ambiente confortável.

#### Regras Fuzzy para Controle de Temperatura:
- Se a temperatura é **fria**, então a intensidade do aquecedor deve ser **baixa**.
- Se a temperatura é **morna**, então a intensidade do aquecedor deve ser **média**.
- Se a temperatura é **quente**, então o ar-condicionado deve ser **alto**.

### Aplicação da Lógica Fuzzy:
A lógica fuzzy permite ajustar as variáveis de entrada, como "muito quente" ou "muito frio", com graus de pertinência, sem a necessidade de valores exatos. O sistema pode então tomar decisões de controle de forma mais flexível.

## 4. Demonstração Prática com Python

Abaixo está o código em Python que implementa um sistema de controle de temperatura utilizando lógica fuzzy.

### Código:

```python
from fuzzywuzzy import fuzz, process

def fuzzy_search(query, choices, threshold=85):
    """
    Realiza uma pesquisa fuzzy na lista de escolhas.
    
    :param query: Termo de pesquisa inserido pelo usuário.
    :param choices: Lista de palavras disponíveis para pesquisa.
    :param threshold: Mínimo de similaridade para considerar uma correspondência.
    :return: Lista de correspondências com pontuação acima do threshold.
    """
    results = process.extract(query, choices, limit=5)
    return [match for match in results if match[1] >= threshold]

# Lista com os 100 jogos mais jogados no mundo
data = [
    "Minecraft", "Grand Theft Auto V", "Tetris", "Wii Sports", "PUBG", "Super Mario Bros.", "Overwatch", 
    "League of Legends", "Fortnite", "The Legend of Zelda: Breath of the Wild", "Call of Duty: Warzone", 
    "Animal Crossing: New Horizons", "Roblox", "Among Us", "Counter-Strike: Global Offensive", "Apex Legends", 
    "Red Dead Redemption 2", "The Witcher 3: Wild Hunt", "Genshin Impact", "Call of Duty: Modern Warfare", 
    "Super Smash Bros. Ultimate", "Dota 2", "Cyberpunk 2077", "Halo Infinite", "Resident Evil Village", 
    "Elden Ring", "Battlefield 2042", "God of War (2018)", "Fall Guys", "FIFA 23", "NBA 2K23", "Valorant", 
    "Destiny 2", "Monster Hunter: World", "Hearthstone", "ARK: Survival Evolved", "The Sims 4", "Dead by Daylight", 
    "Rocket League", "World of Warcraft", "Horizon Forbidden West", "Madden NFL 23", "Rust", "Far Cry 6", 
    "Final Fantasy XIV", "The Elder Scrolls V: Skyrim", "Sea of Thieves", "Forza Horizon 5", "Splatoon 3", 
    "Diablo III", "Assassin's Creed Valhalla", "Ghost of Tsushima", "Pokémon GO", "Pokémon Scarlet and Violet", 
    "Super Mario Odyssey", "Metroid Dread", "Kirby and the Forgotten Land", "Fire Emblem: Three Houses", 
    "Mario Kart 8 Deluxe", "Persona 5 Royal", "Bloodborne", "Dark Souls III", "Sekiro: Shadows Die Twice", 
    "Nioh 2", "Hollow Knight", "Celeste", "Stardew Valley", "Terraria", "Cuphead", "Undertale", "INSIDE", 
    "Little Nightmares", "It Takes Two", "A Way Out", "The Last of Us Part II", "The Last of Us Remastered", 
    "Uncharted 4: A Thief's End", "Spider-Man (PS4/PS5)", "Spider-Man: Miles Morales", "Control", "Death Stranding", 
    "BioShock Infinite", "Portal 2", "Half-Life: Alyx", "DOOM Eternal", "XCOM 2", "Civilization VI", 
    "Age of Empires IV", "Total War: Warhammer III", "StarCraft II", "F1 22", "Gran Turismo 7", 
    "Need for Speed: Heat", "Shadow of the Tomb Raider", "NieR: Automata", "Yakuza: Like a Dragon", "Dragon Ball FighterZ", 
    "Mortal Kombat 11", "Street Fighter V", "Guilty Gear -Strive-"
]

# Lista com variações de "sim"
data_yes = [
    "sim", "yes", "yeah", "yep", "yup", "sure", "of course", "definitely",
    "absolutely", "certainly", "affirmative", "roger", "aye", "uh-huh", 
    "ok", "okay", "indeed", "right", "correct", "claro", "com certeza",
    "pois não", "óbvio", "lógico", "sem dúvida", "beleza", "tá bom",
    "tá certo", "vai nessa", "bora", "boto fé", "concordo", "aceito",
    "d'accord", "oui", "ja", "si", "да", "是的", "はい", "예"
]

# Lista com variações de "não"
data_no = [
    "não", "no", "nah", "nope", "never", "not at all", "definitely not",
    "absolutely not", "negative", "nunca", "nem pensar", "de jeito nenhum",
    "não mesmo", "tá doido", "tô fora", "sem chance", "esquece", "nananina não",
    "d'accord pas", "nein", "non", "nie", "нет", "いいえ", "아니요", "不"
]

# Loop para permitir que o usuário faça várias pesquisas
while True:
    # Entrada do usuário
    query = input("Digite o termo de pesquisa: ")

    # Executa a pesquisa fuzzy nos diferentes conjuntos de dados
    matches_games = fuzzy_search(query, data)
    matches_yes = fuzzy_search(query, data_yes)
    matches_no = fuzzy_search(query, data_no)

    # Exibe os resultados
    if matches_games:
        print("Resultados encontrados nos jogos:")
        for match in matches_games:
            print(f"{match[0]} (Similaridade: {match[1]}%)")
    else:
        print("Nenhuma correspondência encontrada.")

    # Pergunta se o usuário deseja continuar
    continuar = input("\nDeseja fazer outra pesquisa? (sim/não): ").strip().lower()
    if continuar not in data_yes:
        break

print("Obrigado por usar o sistema de pesquisa fuzzy!")
``` 

## 5. Conclusão

A lógica fuzzy é uma ferramenta poderosa para lidar com sistemas imprecisos e incertezas. No exemplo de controle de temperatura, a utilização da lógica fuzzy torna o sistema mais flexível e robusto, permitindo ajustes suaves na intensidade do ar-condicionado baseado nas condições do ambiente. A implementação prática foi realizada utilizando a biblioteca `scikit-fuzzy`, que oferece recursos para construir e simular sistemas de controle fuzzy de forma eficiente.

A lógica fuzzy é especialmente útil em sistemas de IA, onde a precisão exata dos dados não é possível ou necessária. Seu uso pode melhorar a performance de sistemas autônomos e inteligentes, tornando-os mais adaptáveis a diferentes condições e variáveis incertas.
