# ai_app
KICT mini-project

---

# 어린이 동화책 요약 및 번역 앱

<aside>
👉 Team “ai_app”: 신민철, 이영준, 정도영

</aside>

# 과제 개요

---

### 이 프로그램은 영어로 된 어린이 동화책을 한국어 오디오북으로 변환하는 도구입니다. 주요 기능은 다음과 같습니다:

1. 사용자가 어린이 동화책 PDF 파일을 업로드할 수 있습니다.
2. 프로그램이 PDF에서 텍스트를 추출합니다.
3. 인공지능(gpt-4o-mini)을 사용하여 이야기의 핵심 내용을 파악하고 요약합니다. 주요 등장인물, 줄거리, 주제, 교훈 등에 초점을 맞춥니다.
4. 요약된 내용을 한국어로 번역합니다. 이 과정에서도 인공지능을 활용하여 어린이에게 적합한 언어로 번역하고 원작의 스타일을 유지합니다.
5. 마지막으로, 한국어로 번역된 내용을 음성으로 변환합니다.
6. 프로그램 사용 중 사용자는 추출된 텍스트, 요약된 내용, 한국어 번역본을 볼 수 있으며, 번역된 이야기의 오디오 버전도 들을 수 있습니다.

이 도구는 영어 어린이 책을 한국어를 사용하는 어린이들이 접할 수 있게 하거나, 언어 학습 목적으로 활용할 수 있습니다.

# 기술 학습 목표

- Github에 Organization Repository를 생성하고 버전관리 프라이빗 개발환경을 팀내 공유
- Org Repo를 바탕으로 접근 권한이 제어된 Streamlit Web App을 개발
- OpenAI API를 통해 ChatGPT LLM을 활용
- 프롬프트 엔지니어링을 통해 어린이 동화책 요약 및 번역에 특화된 앱 개발

# 기능 상세

---

- 텍스트 추출
- 메인 컨텐트 요약
- 한국어 번역
- 오디오 출력 및 재생
    
# 결과 보고

---

- Github Org Repo를 활용해 팀 프로젝트를 성공적으로 수행했다.
- OpenAI API를 사용해 요약, 번역, 음성 출력 기능을 구현했다.
- Streamlit을 사용해 Web App을 성공적으로 구현했다.
- 프롬프트 엔지니어링을 활용해 어린이 동화책과 영한 번역에 특화된 앱을 구현했다.

---

✨ 요약 프롬프트:

```python
def extract_main_content_with_gpt(text):
    response = client.chat.completions.create(
        model="gpt-4o-mini",  # Updated to gpt-4o-mini
        messages=[
            {"role": "system", "content": """You are an expert in children's literature and story analysis. 
            Your task is to carefully read through a storybook and extract only the main content, 
            focusing on the key elements that make up the story's narrative.

            Please follow these guidelines:
            1. Identify the main characters and their roles in the story.
            2. Summarize the primary plot points and the overall story arc.
            3. Capture any significant themes or morals present in the story.
            4. Note any recurring symbols or motifs that are central to the narrative.
            5. Exclude minor details, repetitive elements, or descriptions that aren't crucial to understanding the core story.
            6. Maintain the essence of the story's language and tone, especially if it's distinctive.
            7. If there are illustrations, briefly mention their significance only if they add crucial information not present in the text.

            Your output should be a concise yet comprehensive representation of the story's main content, 
            suitable for someone who wants to understand the core narrative without reading the entire book."""},
            {"role": "user", "content": f"Please extract the main content from this storybook:\n\n{text}"}
        ],
        max_tokens=2000
    )
    return response.choices[0].message.content
```

✨ 번역 프롬프트:

```python
def translate_text_with_gpt(extracted_text):
    response = client.chat.completions.create(
        model="gpt-4o-mini",  # Updated to gpt-4o-mini
        messages=[
            {"role": "system", "content": """You are an expert translator specializing in children's literature. 
            Your task is to translate the main content of a storybook from English to Korean. 
            Please ensure that you:
            1. Maintain the story's tone and style in the target language.
            2. Accurately convey the main plot points, characters, and themes.
            3. Adapt any cultural references or idioms appropriately for a Korean audience.
            4. Preserve the essence of any moral lessons or educational content.
            5. Keep the language appropriate for the intended age group of the original story."""},
            {"role": "user", "content": f"Please translate the following extracted main content of a storybook to Korean:\n\n{extracted_text}"}
        ],
        max_tokens=2000
    )
    return response.choices[0].message.content
```

# 확장 프로젝트

- [ ]  Figma를 활용한 앱 디자인 개선
- [ ]  pdf를 벗어난 다양한 입력 지원
- [ ]  다국어 지원
- [ ]  audio 음성선택 등 다양한 출력 지원

---

# 결과보고서 제출 과제

✨ Streamlit app

<aside>
👉 https://kict-ai-app.streamlit.app/

</aside>

✨ Github Repo

<aside>
👉 https://github.com/kict-ai-app/ai_app

</aside>
