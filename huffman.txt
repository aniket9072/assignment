import heapq
import time

class HuffmanNode:
    def __init__(self, symbol, freq):
        self.symbol = symbol
        self.freq = freq
        self.left = None
        self.right = None

    def __lt__(self, other):
        return self.freq < other.freq

def build_huffman_tree(data, frequencies):
    priority_queue = [HuffmanNode(data[i], frequencies[i]) for i in range(len(data))]
    heapq.heapify(priority_queue)

    while len(priority_queue) > 1:
        left = heapq.heappop(priority_queue)
        right = heapq.heappop(priority_queue)
        merged_node = HuffmanNode(None, left.freq + right.freq)
        merged_node.left = left
        merged_node.right = right
        heapq.heappush(priority_queue, merged_node)

    return priority_queue[0]

def build_huffman_codes(root, current_code, huffman_codes):
    if root is None:
        return

    if root.symbol is not None:
        huffman_codes[root.symbol] = current_code
    build_huffman_codes(root.left, current_code + '0', huffman_codes)
    build_huffman_codes(root.right, current_code + '1', huffman_codes)

def encode(data, huffman_codes):
    encoded_data = ""
    for symbol in data:
        if symbol in huffman_codes:
            encoded_data += huffman_codes[symbol]
    return encoded_data

def decode(encoded_data, root):
    decoded_data = ""
    current_node = root
    for bit in encoded_data:
        if bit == '0':
            current_node = current_node.left
        else:
            current_node = current_node.right

        if current_node is not None and current_node.symbol is not None:
            decoded_data += current_node.symbol
            current_node = root  

    return decoded_data


def display_huffman_tree(root, prefix="", is_left=True):
    if root is not None:
        print(prefix + ("|-- " if is_left else "`-- ") + str(root.symbol) + f" ({root.freq})")
        display_huffman_tree(root.left, prefix + ("|   " if is_left else "    "), True)
        display_huffman_tree(root.right, prefix + ("|   " if is_left else "    "), False)


data = input("Enter the symbols (e.g., A B C D): ").split()
frequencies = list(map(int, input("Enter the frequencies for each symbol: ").split()))

start = time.time()
if len(data) != len(frequencies):
    print("Number of symbols and frequencies should match.")
else:
    root = build_huffman_tree(data, frequencies)
    huffman_codes = {}
    build_huffman_codes(root, '', huffman_codes)

    print("Huffman Tree:")
    display_huffman_tree(root)

    print("\nHuffman Codes:")
    for symbol, code in huffman_codes.items():
        print(f"{symbol}: {code}")

    message = input("Enter a message to encode: ")
    encoded_message = encode(message, huffman_codes)
    print(f"Encoded Message: {encoded_message}")

    decoded_message = decode(encoded_message, root)
    print(f"Decoded Message: {decoded_message}")
end = time.time()
print("Time Complextiy: ",end-start)