 Reggie's Linear Regression Project

# Part 1: Calculating Error

def get_y(m, b, x):
    return m * x + b

# Test get_y()
#print(get_y(1, 0, 7))  # 7
#print(get_y(5, 10, 3))  # 25
#print(get_y(-1, 0, 2))  # -2
#print(get_y(0, 0, 5))  # 0

def calculate_error(m, b, point):
    x_point = point[0]
    y_point = point[1]
    y_line = get_y(m, b, x_point)
    return abs(y_line - y_point)

# Test calculate_error()
#print(calculate_error(1, 0, (3, 3)))  # 0
#print(calculate_error(1, 0, (3, 4)))  # 1
#print(calculate_error(1, -1, (3, 3)))  # 1
#print(calculate_error(-1, 1, (3, 3)))  # 5

# Dataset
datapoints = [(1, 2), (2, 0), (3, 4), (4, 4), (5, 3)]

def calculate_all_error(m, b, points):
    total_error = 0
    for point in points:
        total_error += calculate_error(m, b, point)
    return total_error

# Test calculate_all_error()
#print(calculate_all_error(1, 0, datapoints))
#print(calculate_all_error(0, 0, datapoints))
#print(calculate_all_error(1, 1, datapoints))

# Part 2: Try a bunch of slopes and intercepts!
possible_ms = [m * 0.1 for m in range(-100, 101)]
possible_bs = [b * 0.1 for b in range(-200, 201)]

smallest_error = float('inf')
best_m = 0
best_b = 0

for m in possible_ms:
    for b in possible_bs:
        error = calculate_all_error(m, b, datapoints)
        if error < smallest_error:
            best_m = m
            best_b = b
            smallest_error = error

print("Best m:", best_m)
print("Best b:", best_b)
print("Smallest error:", smallest_error)

# Part 3: Prediction
prediction = get_y(best_m, best_b, 6)
print("Prediction for x = 6:", prediction)
