# 🐹 Capibara-LLM

[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)
[![Hugging Face](https://img.shields.io/badge/🤗%20Hugging%20Face-Organization-yellow)](https://huggingface.co/Capibara-LLM)
[![Python](https://img.shields.io/badge/Python-3.9%2B-green)](https://www.python.org/)

> **Inteligencia Artificial con identidad paraguaya.**

Bienvenido al repositorio oficial de **Capibara-LLM**, una iniciativa Open Source dedicada al desarrollo de Modelos de Lenguaje (LLMs) y Datasets para el idioma **Guaraní** y su variante **Jopará**.

Al igual que el Capibara, buscamos ser una comunidad social, tranquila y amigable con el ecosistema open-source.

---

## 🎯 Nuestra Misión

El Guaraní es un idioma considerado "low-resource" en el mundo de la IA actual. En **Capibara-LLM** trabajamos para cambiar eso mediante tres pilares:

1.  **Recopilación de Datos:** Creación y curaduría de los datasets más extensos de Guaraní-Jopará existentes hasta la fecha.
2.  **Fine-Tuning:** Adaptación de modelos estado del arte (Gemma, Llama, Qwen, Mistral) para que entiendan el contexto cultural y lingüístico de Paraguay.
3.  **Cultura:** Preservar la riqueza lingüística de Paraguay en la era digital.

---

## 🚀 Modelos (The Capibara Zoo)

Nuestros modelos están alojados en Hugging Face, pero puedes integrarlos en tu código desde aquí.

| Modelo | Base | Descripción | Link |
| :--- | :--- | :--- | :--- |
| **Gemma-2-9B-It-SimPO-Jopara** | Gemma 2 9B | Modelo insignia optimizado con SimPO para instrucciones en Guaraní-Jopará. | [🤗 Ver Modelo](https://huggingface.co/Capibara-LLM/gemma-2-9b-it-SimPO-Jopara) |

### 💻 Ejemplo de Uso (Inferencia)

Puedes correr nuestro modelo insignia utilizando `transformers`:

```python
import torch
from transformers import AutoTokenizer, AutoModelForCausalLM

# Identificador del modelo en Hugging Face
model_id = "Capibara-LLM/gemma-2-9b-it-SimPO-Jopara"

tokenizer = AutoTokenizer.from_pretrained(model_id)
model = AutoModelForCausalLM.from_pretrained(
    model_id,
    torch_dtype=torch.bfloat16,
    device_map="auto",
)

messages = [
    {"role": "user", "content": "Mba'éichapa, ¿podrías explicarme qué es el tereré?"},
]

input_ids = tokenizer.apply_chat_template(messages, return_tensors="pt", add_generation_prompt=True).to("cuda")

outputs = model.generate(
    input_ids,
    max_new_tokens=256,
    do_sample=True,
    temperature=0.7,
)

print(tokenizer.decode(outputs[0][input_ids.shape[-1]:], skip_special_tokens=True))
````

-----

## 📚 Datasets

La comida de nuestros Capibaras. Estos datasets han sido procesados para entrenamiento de LLMs:

  * 📂 **[Capibara-LLM/dataset-guarani-jopara-v01](https://huggingface.co/datasets/Capibara-LLM/dataset-guarani-jopara-v01)**: Dataset de instrucciones estilo Alpaca traducido y adaptado al Guaraní-Jopará.
  * 📂 **[Capibara-LLM/gn-multi-affective-alpaca](https://huggingface.co/datasets/Capibara-LLM/gn-multi-affective-alpaca)**: Corpus masivo limpio de fuentes web y literatura, enfocado en análisis de sentimiento y tareas generales.

**Cómo cargar los datos en Python:**

```python
from datasets import load_dataset

# Cargar el dataset de instrucciones
ds = load_dataset("Capibara-LLM/dataset-guarani-jopara-v01")
print(ds['train'][0])
```

-----

## 🛠️ Instalación y Desarrollo

Para colaborar con el código de este repositorio (scripts de limpieza, entrenamiento, evaluación):

1.  Clona el repositorio:

    ```bash
    git clone https://github.com/Capibara-LLM/Capibara-LLM.git
    cd capibara-llm
    ```

2.  Instala las dependencias:

    ```bash
    pip install -r requirements.txt
    ```

-----

## 🤝 Únete a la Manada

Estamos buscando colaboradores tanto técnicos como lingüísticos.

  * **Desarrolladores:** Ayuda a limpiar datos, optimizar scripts de entrenamiento o crear demos.
  * **Hablantes Nativos:** Ayuda a validar las respuestas de nuestros modelos y corregir traducciones.

Consulta nuestro [CONTRIBUTING.md](CONTRIBUTING.md) para saber cómo empezar.

-----

## 📄 Licencia

Este proyecto se distribuye bajo la licencia **Apache 2.0**.

-----

*Hecho con 🧉 y ❤️ desde Paraguay.*
