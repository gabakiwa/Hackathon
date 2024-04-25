Hackathon 2024, Desafio Hiperstream
Equipe: Conexão / Código HIPER-177
Integrantes: - Amanda Pageu Silva
             - Gabriel Akira Wakavaiachi
             - Renan Yudi Fukumori
             
Link para Código: https://colab.research.google.com/drive/1P7EtRSQFhTYdtw6444ziUyVkZWtBE4cy?usp=sharing

Código 1:

import graphviz as gz 
import pandas as pd
import re

url = "https://raw.githubusercontent.com/gabakiwa/Hackathon/main/baseparateste-1.csv" 
Base = pd.read_csv(url)

grafo = {}
dot = gz.Digraph(graph_attr={'rankdir': 'LR'}) 
for _, row in Base.iterrows():
    aplicacao = re.sub(r"[^\w:/-]", "", row["Nome"])
    origem = re.sub(r"\W", "", row["PastaOrigem"])
    destino =  re.sub(r"\W", "", row["PastaDestino"]) if not pd.isnull(row['PastaDestino']) else ""  
    
    if backup is not None:
       
        if origem not in grafo:
            grafo[origem] = []
            
            label = f"{origem}\n{row['Nome']}" 
            dot.node(origem, label=label) 
        
        grafo[origem].append(destino)
        
        dot.node(destino)  

for k, v in grafo.items(): 
    for n in v: 
        dot.edge(k, n)

dot.attr(rank='same')
for i, node in enumerate(grafo.keys()):
    dot.attr(rank='same', _attributes={'rank': 'same', 'same': f'{node};'}) 

dot.render('OrigemDestino', format='pdf', cleanup=True) 
print("Diagrama do grafo dividido em camadas verticais gerado com sucesso como 'OrigemDestino.pdf'")


Código 2:

import graphviz as gz 
import pandas as pd
import re

url = "https://raw.githubusercontent.com/gabakiwa/Hackathon/main/baseparateste-1.csv" 
Base = pd.read_csv(url)

grafo = {}
dot = gz.Digraph(graph_attr={'rankdir': 'LR'}) 
for _, row in Base.iterrows():
    aplicacao = re.sub(r"[^\w:/-]", "", row["Nome"])
    origem = re.sub(r"\W", "", row["PastaOrigem"])
    backup =  re.sub(r"\W", "", row["PastaBackup"]) if not pd.isnull(row['PastaBackup']) else ""  
    
    if backup is not None:
       
        if origem not in grafo:
            grafo[origem] = []
            
            label = f"{origem}\n{row['Nome']}" 
            dot.node(origem, label=label) 
        
        grafo[origem].append(backup)
        
        dot.node(backup)  
        
        grafo[origem].append(backup)
        
        dot.node(backup)  

for k, v in grafo.items(): 
    for n in v: 
        dot.edge(k, n)

dot.attr(rank='same')
for i, node in enumerate(grafo.keys()):
    dot.attr(rank='same', _attributes={'rank': 'same', 'same': f'{node};'}) 
    
dot.render('OrigemBackup', format='pdf', cleanup=True) 
print("Diagrama do grafo dividido em camadas verticais gerado com sucesso como 'OrigemBackup.pdf'")
