# Tokkit - AI Assited, Interactive Learning Helper

<img width="960" alt="Group 1948755841" src="https://github.com/user-attachments/assets/993ee15e-0c24-48e8-9bad-3bd8ea08e637" />

## 📖 Project Background

Explaining what you've learned in your own words is one of the most effective ways to enhance learning. This is known in psychology as the **"Teaching Effect"** — a method proven to improve memory retention and deepen understanding more effectively than simply reading or taking notes.

In fact, many students review and memorize material by summarizing it out loud. **Tokkit** is an interactive learning assistant application designed to support this process in a more structured way.

When a student explains what they’ve studied to the AI, the AI provides feedback and automatically generates notes based on the explanation. Tokkit also notifies users of optimal review times based on the forgetting curve, and helps reinforce learning through features like quizzes.

## 🔧 Architecture

<img src="https://i.imgur.com/mnfWKYE.png" width="720" />

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


## 🍟 Team - OGAMJA

| 홍해담(팀장) | 남윤혁 | 박진성 | 임차민 | 최승재 |
|:---:|:---:|:---:|:---:|:---:|
| <a href="https://github.com/hhd1337" target="_blank"><img width="128" src="https://avatars.githubusercontent.com/u/181053444?s=96&v=4" /></a> | <a href="https://github.com/nyhryan" target="_blank"><img width="128" src="https://avatars.githubusercontent.com/u/85018069?s=96&v=4" /></a> | <a href="https://github.com/Jinseong01" target="_blank"><img width="128" src="https://avatars.githubusercontent.com/u/147074506?s=96&v=4" /></a> | <a href="https://github.com/ckals413" target="_blank"><img width="128" src="https://avatars.githubusercontent.com/u/124526270?s=96&v=4" /></a> | <a href="https://github.com/seungjae708" target="_blank"><img width="128" src="https://avatars.githubusercontent.com/u/64647590?s=96&v=4" /></a> |
| Backend | Backend | Backend | Frontend | Frontend |

> Click the profile images to visit members' repository!

### Backend

- 홍해담: Responsible for review and comment APIs, integration with external APIs, and push notifications using `Firebase`
- 남윤혁: Handles integration with the Vector Database (`Milvus`), and implements search and recommendation algorithms using the vector DB
- 박진성: In charge of user authentication (`Spring Security + JWT`), deployment environment setup (`Docker + AWS EC2`), and CI/CD pipeline using `GitHub Actions`

### Frontend

- 임차민: Designs and implements UI/UX for notes and conversations, and ports on-device models via `Qualcomm AI Hub`
- 최승재: Designs and implements UI/UX for home and review pages, and ports on-device models via `Qualcomm AI Hub`
