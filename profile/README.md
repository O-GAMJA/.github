# Tokkit - AI Assited, Interactive Learning Helper

<img width="960" alt="Group 1948755841" src="https://github.com/user-attachments/assets/993ee15e-0c24-48e8-9bad-3bd8ea08e637" />

## 📖 Project Background

Explaining what you've learned in your own words is one of the most effective ways to enhance learning. This is known in psychology as the **"Teaching Effect"** — a method proven to improve memory retention and deepen understanding more effectively than simply reading or taking notes.

In fact, many students review and memorize material by summarizing it out loud. **Tokkit** is an interactive learning assistant application designed to support this process in a more structured way.

When a student explains what they’ve studied to the AI, the AI provides feedback and automatically generates notes based on the explanation. Tokkit also notifies users of optimal review times based on the forgetting curve, and helps reinforce learning through features like quizzes.

## 🔧 Architecture

![image](https://github.com/user-attachments/assets/0290c005-bbf9-4aff-a71f-1bf6f9977d31)

The user explains what they are currently studying about with Tokkit Android application. `llama3-3b` model is **fully running On-Device mode**. No network API calls for external AI models. (* Devices with supported chipset(`e.g. Galaxy S25`)) only)

During the conversation session, Tokkit responds to the user giving some feedback on the user's explanation. `llama3-3b` is used here.

After the session, the summary note is generated with a Markdown format, based on the session's data. `llama3-3b` is used here as well.

The banner images of the note are created Stable Diffusion 2.1 model, also running On-Device.

If the user agrees to share the generated note with other users, the note will be uploaded to the server. The note will be processed and saved to the vector database.

When the user wants to search other users' notes(*sharing your knowledge is good!*), vector database is used to fetch the search results.

## 🧰 Technologies

### Frontend

- Languages / Frameworks
  - Kotlin
  - Android SDK
  - Genie SDK(C++)
- Tools
  - Android Studio
  - [Qualcomm AI Hub](https://aihub.qualcomm.com/)
  - Firebase - Mobile push notifications
- Models(from Qualcomm AI Hub)
  - llama 3.2:3B
  - Stable Diffusion 2.1

 ### Backend

- Languages / Frameworks
  - Spring Boot 6 /w RESTful API
  - Spring Security /w JWT Authentication
  - JDK 21
  - MySQL - Relational Database
  - Milvus - Vector Database
  - Redish - Cache Storage
 - Tools
   - IntelliJ IDEA
   - Docker
 - Models(API)
   - text-embedding-ada-002(Embedding)
   - GPT 4o Mini TTS(Lecture audio generation)
   - GPT 4.1 Mini(Quiz generation)
   - GPT 3.5 Turbo(Translation KR->EN)
   - Clova OCR

## 📝 Implementation Details

### Frontend

1. Transcribes the user's voice with Android Speech-to-Text feature into the text
2. Embeds the transcription into the prompt, then feed the prompt into `llama3-3b` model(Running **On-Device**, no network needed)
3. Then the LLM's generated response is read with Android Text-to-Speech to give the user the feeling that the user is having a conversation with someone
4. After the session, `llama3-3b` is once more used to generate the study note

### Backend

1. When the user's note is uploaded to the server, the note is saved to the Vector Database
2. Keyword search and *'Find similar notes with this note'* search is implemented using Vector Database's vector field search
3. Recommended note for each user(just like YouTube home feed) is implemented through calculating the user's interest vector, then search the Vector Database with the vector.

## 📖 Recommended Notes algorithm

![image](https://github.com/user-attachments/assets/acb00670-9ad9-459e-b5cb-46ca3b9e0687)

The user's interests are represented by the **mean vector of all note embeddings** they have created.

---

![image](https://github.com/user-attachments/assets/03f902b0-f828-4cea-abd8-6043410d5bff)

To generate recommendations, the mean vector of a user's note embeddings is used to perform a similarity search against other notes stored in the vector database.

The retrieved results are subsequently re-ranked based on **tag relevance**. A user's tag frequency distribution serves as an indicator of current interests—notes that share more tags with higher frequency in the user's tag map are considered more relevant. 

Tag similarity is measured using [Weighted Jaccard Similarity](https://en.wikipedia.org/wiki/Jaccard_index#Weighted_Jaccard_similarity_and_distance), which accounts for both the presence and frequency of tags. This ensures that notes containing commonly used tags by the user are given higher priority in the final recommendation list.

## 🍟 Team - OGAMJA

| 홍해담(팀장) | 남윤혁 | 박진성 | 임차민 | 최승재 |
|:---:|:---:|:---:|:---:|:---:|
| <a href="https://github.com/hhd1337" target="_blank"><img width="128" src="https://avatars.githubusercontent.com/u/181053444?s=96&v=4" /></a> | <a href="https://github.com/nyhryan" target="_blank"><img width="128" src="https://avatars.githubusercontent.com/u/85018069?s=96&v=4" /></a> | <a href="https://github.com/Jinseong01" target="_blank"><img width="128" src="https://avatars.githubusercontent.com/u/147074506?s=96&v=4" /></a> | <a href="https://github.com/ckals413" target="_blank"><img width="128" src="https://avatars.githubusercontent.com/u/124526270?s=96&v=4" /></a> | <a href="https://github.com/seungjae708" target="_blank"><img width="128" src="https://avatars.githubusercontent.com/u/64647590?s=96&v=4" /></a> |
| Backend | Backend | Backend | Frontend | Frontend |

> Click the profile images to visit members' repository!

### Backend

- 홍해담: Implements review and comment APIs, integration with external APIs, and push notifications using `Firebase`
- 남윤혁: Handles integration with the Vector Database (`Milvus`), and implements search and recommendation algorithms using the vector DB
- 박진성: In charge of user authentication (`Spring Security + JWT`), deployment environment setup (`Docker + AWS EC2`), and CI/CD pipeline using `GitHub Actions`

### Frontend

- 임차민: Designs and implements UI/UX for notes and conversations, and ports on-device models via `Qualcomm AI Hub`
- 최승재: Designs and implements UI/UX for home and review pages, and ports on-device models via `Qualcomm AI Hub`

## 🎞️ Demo Video

[![Tokkit Demo](https://img.youtube.com/vi/U1QxSzgBspc/0.jpg)](https://www.youtube.com/watch?v=U1QxSzgBspc)

> 📺 Click the image above to watch the YouTube demo — see how Tokkit helps learners turn their spoken explanations into structured, review-ready notes, all powered by on-device AI.


