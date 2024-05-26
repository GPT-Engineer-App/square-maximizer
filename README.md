# square-maximizer

def solution(A):
    # 配列が空の場合、0を返す
    if not A or not A[0]:
        return 0
    
    N = len(A)  # 行の数
    M = len(A[0])  # 列の数
    
    dp = [[0] * M for _ in range(N)]  # 二次元配列を作る
    largest_squares = []  # 一番大きい正方形のリスト

    # dp配列を埋める
    for i in range(N):
        for j in range(M):
            if A[i][j]:  # Trueの場合
                if i == 0 or j == 0:
                    dp[i][j] = 1  # 端の行または列なら1
                else:
                    dp[i][j] = min(dp[i-1][j], dp[i][j-1], dp[i-1][j-1]) + 1  # 左、上、左上の最小値 + 1
                
                largest_squares.append((dp[i][j], i, j))  # 全ての正方形をリストに追加

    # 正方形のサイズで降順に並べ替え
    largest_squares.sort(reverse=True, key=lambda x: x[0])

    # Function to check if two squares overlap
    def overlap(sq1, sq2):
        size1, x1, y1 = sq1
        size2, x2, y2 = sq2
        return not (x1 - size1 >= x2 or x2 - size2 >= x1 or y1 - size1 >= y2 or y2 - size2 >= y1)
    
    # Find the two largest non-overlapping squares
    max_area = 0
    for i in range(len(largest_squares)):
        for j in range(i + 1, len(largest_squares)):
            if not overlap(largest_squares[i], largest_squares[j]):
                max_area = max(max_area, largest_squares[i][0] * largest_squares[i][0])
                return max_area  # Return the area as soon as we find the largest non-overlapping squares
    
    return 0  # 正方形が見つからなければ0を返す

# Example usage:
A1 = [
    [False, True, False, True],
    [True, True, True, False],
    [True, True, True, True],
    [False, True, True, True]
]

A2 = [
    [True, True, True, True],
    [True, True, True, True],
    [True, True, True, True],
    [True, True, True, True],
    [True, True, True, True],
    [True, True, True, True]
]

A3 = [
    [False, False, False, False, False],
    [False, False, True, False, False],
    [False, False, False, False, False]
]

print(solution(A1))  # Should return 4
print(solution(A2))  # Should return 9
print(solution(A3))  # Should return 0


## Collaborate with GPT Engineer

This is a [gptengineer.app](https://gptengineer.app)-synced repository 🌟🤖

Changes made via gptengineer.app will be committed to this repo.

If you clone this repo and push changes, you will have them reflected in the GPT Engineer UI.

## Tech stack

This project is built with React and Chakra UI.

- Vite
- React
- Chakra UI

## Setup

```sh
git clone https://github.com/GPT-Engineer-App/square-maximizer.git
cd square-maximizer
npm i
```

```sh
npm run dev
```

This will run a dev server with auto reloading and an instant preview.

## Requirements

- Node.js & npm - [install with nvm](https://github.com/nvm-sh/nvm#installing-and-updating)
