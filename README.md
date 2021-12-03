# EEE3314_Segmentation_Challenge
기초인공지능 의료영상 챌린지

---
# Reference
- http://proceedings.mlr.press/v85/lu18a/lu18a.pdf
- https://re-code-cord.tistory.com/m/entry/%EC%9E%AC%ED%99%9C%EC%9A%A9-%ED%92%88%EB%AA%A9-%EB%B6%84%EB%A5%98%EB%A5%BC-%EC%9C%84%ED%95%9C-Semantic-Segmentation-%EB%8C%80%ED%9A%8C-23 (DenseCRF 적용)
- https://www.kakaobrain.com/blog/48
- https://brunch.co.kr/@kakao-it/77
- https://yhu0409.tistory.com/9 (Few dataset solution)

---

# 진행상황
- *Unet_hands_on(epoch=200,_pretrained=False, num_classes=7).ipynb* 에서 multi-class segmentation을 구현하여 결과를 출력하였다.
- Background와 S1은 prediction을 잘 했는데 L1,L2,L3,L4,L5는 잘 prediction하지 못했다.
## 개선점
- Lumbar Spine이 왜 겹쳐서 인식되는걸까? -> Image preprocess 문제?, Mask preprocess 문제?
- 일단 가장 먼저 Mask data를 jpg말고 png로 저장하기 -> 완료
- Val data 올라온거 다운받고 다시 돌려보기 -> Val data에 라벨 없음, 제출용 데이터
- Image data를 선명하게 해볼까?
- K-Fold Cross Validation?

- 흑백 반전된 데이터가 조금 들어있음(78, 84, 90, 97, 103, 119번 이미지)
- 1. threshold 정해서 흑백반전시키기 -> 경계가 그리 명확하지 않아서 힘들듯, 107번은 103번보다 오히려 avg가 더 큼
- 2. 테두리를 그린 이미지를 학습시키기

---

# Preprocess
### 데이터 불러오기
- dcm을 numpy로 불러올 때 pydicom 라이브러리 사용하면 오류뜸

# EDA
- 흑백반전 + 좌우반전(테스트셋엔 얼마나 있을진 모르겠으나 제출용 데이터셋에 좌우반전된 데이터 한장이 있었음)
