from collections import deque

initial_state = ('A', 'B', 'floor', False)  
goal_state = True

def is_goal(state):
    return state[3] == True

def get_successors(state):
    monkey_pos, box_pos, status, has_banana = state
    successors = []

    positions = ['A', 'B', 'C']

    if status == 'floor':
        for pos in positions:
            if pos != monkey_pos:
                successors.append((pos, box_pos, 'floor', has_banana))

    if status == 'floor' and monkey_pos == box_pos:
        for pos in positions:
            if pos != monkey_pos:
                successors.append((pos, pos, 'floor', has_banana))

    if monkey_pos == box_pos and status == 'floor':
        successors.append((monkey_pos, box_pos, 'box', has_banana))

    if monkey_pos == 'C' and box_pos == 'C' and status == 'box':
        successors.append((monkey_pos, box_pos, status, True))

    return successors

def bfs():
    queue = deque([initial_state])
    visited = set()

    while queue:
        state = queue.popleft()

        if state in visited:
            continue
        visited.add(state)

        if is_goal(state):
            return state

        for successor in get_successors(state):
            queue.append(successor)

    return None

solution = bfs()
print("Goal Reached:", solution)
