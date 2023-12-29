import tkinter as tk
import time
from queue import PriorityQueue
import math

class MatrixVisualizer:
    def __init__(self, matrix):
        self.matrix = matrix
        self.rows = len(matrix)
        self.cols = len(matrix[0])

        self.root = tk.Tk()
        self.canvas = tk.Canvas(self.root, width=self.cols * 50, height=self.rows * 50)
        self.canvas.pack()

        self.draw_matrix()

    def draw_matrix(self):
        for i in range(self.rows):
            for j in range(self.cols):
                color = "white" if self.matrix[i][j] == 0 else "black"
                self.canvas.create_rectangle(j * 50, i * 50, (j + 1) * 50, (i + 1) * 50, fill=color)
        self.root.update()
        # time.sleep(0.1)

    def update_cell(self, cell, color):
        i, j = cell
        self.canvas.create_rectangle(j * 50, i * 50, (j + 1) * 50, (i + 1) * 50, fill=color)
        self.root.update()
        # time.sleep(0.1)

    def run(self):
        self.root.mainloop()

def find_path(matrix, start, goal, visualizer):
    queue = PriorityQueue()
    visited = set()
    queue.put((0, start, [start]))

    while not queue.empty():
        cost, current, path = queue.get()

        if current in visited:
            continue
        visited.add(current)

        # print("path type : {}".format(type(path)))

        if current == goal:
            for cell in path:
                visualizer.update_cell(cell, "green")
            return path + [next_step]

        for next_step in get_neighbors(matrix, current):
            new_cost = cost + 1
            new_path = path + [next_step] # list의 병합
            queue.put((new_cost + heuristic_e(next_step, goal), next_step, new_path))
            visualizer.update_cell(next_step, "blue")

    return None

def heuristic_m(a, b):
    return abs(a[0] - b[0]) + abs(a[1] - b[1])

def heuristic_e(a, b):
    return math.sqrt(pow(b[0]-a[0] ,2) + pow(b[1]-a[1] ,2))

def get_neighbors(matrix, pos):
    neighbors = []
    for i, j in [(0, 1), (1, 0), (0, -1), (-1, 0)]:
        x, y = pos[0] + i, pos[1] + j
        if 0 <= x < len(matrix) and 0 <= y < len(matrix[0]) and matrix[x][y] == 0:
            neighbors.append((x, y))
    return neighbors

# 매트릭스 예제
matrix = [
    [0, 0, 0, 0, 1, 0, 0],
    [0, 1, 1, 1, 0, 0, 1],
    [0, 0, 0, 1, 0, 1, 0],
    [0, 1, 0, 0, 0, 0, 0],
    [0, 0, 0, 1, 0, 1, 0],
    [0, 0, 0, 1, 0, 1, 0],
    [0, 0, 0, 1, 0, 1, 0]
]

# 시작과 목표 지점
start = (0, 0)
goal = (6, 6)

# Tkinter 시각화 객체 생성
visualizer = MatrixVisualizer(matrix)

# 경로 찾기 및 시각화
start_time = time.time()
path = find_path(matrix, start, goal, visualizer)
end_time = time.time()
print("elapsed time : {}".format(end_time - start_time))
if path:
    print("최단 경로:", path)
else:
    print("경로를 찾을 수 없습니다.")

# Tkinter 실행
visualizer.run()
