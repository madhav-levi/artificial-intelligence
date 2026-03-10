import heapq

GOAL_STATE = [[1, 2, 3],
              [4, 5, 6],
              [7, 8, 0]]

MOVES = [(-1, 0), (1, 0), (0, -1), (0, 1)]


class Puzzle:
    def __init__(self, board, parent=None, move="", depth=0):
        self.board = board
        self.parent = parent
        self.move = move
        self.depth = depth
        self.cost = depth + self.heuristic()

    def heuristic(self):
        distance = 0
        for i in range(3):
            for j in range(3):
                value = self.board[i][j]
                if value != 0:
                    goal_x = (value - 1) // 3
                    goal_y = (value - 1) % 3
                    distance += abs(i - goal_x) + abs(j - goal_y)
        return distance

    def __lt__(self, other):
        return self.cost < other.cost

    def find_zero(self):
        for i in range(3):
            for j in range(3):
                if self.board[i][j] == 0:
                    return i, j

    def generate_children(self):
        children = []
        x, y = self.find_zero()

        for dx, dy in MOVES:
            nx, ny = x + dx, y + dy
            if 0 <= nx < 3 and 0 <= ny < 3:
                new_board = [row[:] for row in self.board]
                new_board[x][y], new_board[nx][ny] = new_board[nx][ny], new_board[x][y]
                children.append(Puzzle(new_board, self, (dx, dy), self.depth + 1))
        return children


def board_to_tuple(board):
    return tuple(tuple(row) for row in board)


def a_star(start_board):
    start_node = Puzzle(start_board)
    open_list = []
    heapq.heappush(open_list, start_node)
    closed_set = set()

    while open_list:
        current = heapq.heappop(open_list)

        if current.board == GOAL_STATE:
            return current

        closed_set.add(board_to_tuple(current.board))

        for child in current.generate_children():
            if board_to_tuple(child.board) not in closed_set:
                heapq.heappush(open_list, child)

    return None


def print_solution(solution):
    path = []
    while solution:
        path.append(solution.board)
        solution = solution.parent
    path.reverse()

    for step in path:
        for row in step:
            print(row)
        print()

start = [[1, 2, 3],
         [4, 0, 6],
         [7, 5, 8]]

solution = a_star(start)

if solution:
    print("Solution found!\n")
    print_solution(solution)
else:
    print("No solution exists.")
