# TESTE_DE_CYBER
Esse projeto e um teste para mim aperfeiçoar a minha habilidade  
import hashlib

def gerar_hash(nome_arquivo):
    "Lê um arquivo e gera sua impressão digital (SHA-256)"
    sha256_hash = hashlib.sha256()

    try:
        with open(nome_arquivo, "rb") as f:
            for byte_block in iter(lambda: f.read(4096), b""):
                sha256_hash.update(byte_block)
        return sha256_hash.hexdigest()
    except FileNotFoundError:
        return None


banco_malwares = {
    "e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855": "Trojan.Generic",
    "5e884898da28047151d0e56f8dc6292773603d0d6aabbdd62a11ef721d1542d8": "Ransomware.Locky"
}

arquivo_para_testar = "logs_servidor.csv"
hash_do_arquivo = gerar_hash(arquivo_para_testar)

if hash_do_arquivo:
    print(f"📄 Arquivo: {arquivo_para_testar}")
    print(f"🔑 Hash SHA-256: {hash_do_arquivo}")

    if hash_do_arquivo in banco_malwares:
        print(f"🚨 ALERTA: Arquivo MALICIOSO detectado! Tipo: {banco_malwares[hash_do_arquivo]}")
    else:
        print("✅ Arquivo íntegro e seguro.")
else:
    print("❌ Arquivo não encontrado.")
   
