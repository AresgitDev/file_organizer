from pathlib import Path
import shutil
from datetime import datetime
selec = input("selecione a pasta a ser organizada:")
caminho = Path(selec)
if caminho.exists() and caminho.is_dir():
    for arquivos in caminho.iterdir():
        if arquivos.is_file() and arquivos.exists():
            ext = arquivos.suffix.lower().replace('.','')
            dest = caminho/ext
            dest.mkdir(exist_ok=True)
            way = dest/arquivos.suffix
            shutil.move(str(arquivos),str(way))
            data_hora = datetime.now().strftime('%d/%m/%Y %H:%M:%S')
            log_linha = f"[{data_hora}] ARQUIVO: {arquivos.name} | DESTINO: {way}\n"
            with open(caminho / "log.txt", "a", encoding="utf-8") as f:
             f.write(log_linha) 
