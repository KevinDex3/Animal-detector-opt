# 🐾 Animal Detector OPT (MobileNetV2)

Questa funzione serverless utilizza **MobileNetV2** pre-addestrato su **ImageNet** per classificare immagini. Restituisce le **prime 3 predizioni** con le rispettive probabilità e gestisce automaticamente il download/salvataggio del modello in locale.

---

## 📦 Funzionalità

- Accetta una richiesta `POST` con `multipart/form-data` contenente un'immagine (`file`)
- Usa `torchvision.models.mobilenet_v2` con i pesi `IMAGENET1K_V1`
- Restituisce le **3 classi più probabili**
- Salva il modello in locale come `mobilenet_v2.pth` alla prima esecuzione
- Controlla se il modello è già disponibile prima di eseguire la classificazione
- Supporta ambienti **serverless** come **OpenFaaS**, **AWS Lambda**, ecc.

---

## 🧠 Esempio di risposta JSON

```json
{
  "top_3_predictions": [
    {"class": "tabby cat", "probability": 0.92},
    {"class": "tiger cat", "probability": 0.06},
    {"class": "Egyptian cat", "probability": 0.01}
  ],
  "model_status": "File modello esiste: /path/to/mobilenet_v2.pth"
}

```

## ⌨️​ Esempio di input

curl -X POST http://INDIRIZZO/function/animal-detector-opt  -H "Content-Type: multipart/form-data"   -F "file=@/home/kevin/Immagini/cane.jpeg"
Occorre prima salvare un'immagine e successivamente specificare il percorso appropriato!
