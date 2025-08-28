## Architecture Diagram

```mermaid
flowchart LR
    subgraph Data_Layer[Data Layer]
        Crawler[crawler/ <br> Scrapes data for series/anime]
        Dataset[(data/ <br> Raw + Processed datasets)]
    end

    subgraph Processing_Layer[Processing / NLP Layer]
        ThemeExtractor[theme_classifier/ <br> Zero-shot Theme Extraction]
        TextClassifier[text_classification/ <br> Supervised Text Classification]
        CharNetwork[character_network/ <br> NER + Graph (spaCy + NetworkX)]
    end

    subgraph Frontend_Layer[Frontend / UI Layer]
        GradioUI[gradio_app.py <br> Web Interface]
        Chatbot[character_chatbot/ <br> LLM Character Chat]
    end

    Crawler --> Dataset
    Dataset --> ThemeExtractor
    Dataset --> TextClassifier
    Dataset --> CharNetwork
    ThemeExtractor --> GradioUI
    TextClassifier --> GradioUI
    CharNetwork --> GradioUI
    GradioUI --> Chatbot
