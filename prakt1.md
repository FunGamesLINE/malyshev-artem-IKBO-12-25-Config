# Задание 1

# Задание 2
awk '{print $2, $1}' protocols | sort -rn | grep "[0-9]" | head -5