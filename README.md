# 1
#include <iostream>
#include <cmath>

void findPythagoreanTriples(int n) {
    for (int a = 1; a <= n; a++) {
        for (int b = a; b <= n; b++) { 
            int cSquared = a*a + b*b;
            int c = std::sqrt(cSquared);
            if (c * c == cSquared && c <= n) {
                std::cout << a << " " << b << " " << c << std::endl;
            }
        }
    }
}

int main() {
    int n;
    std::cout << "Enter n: ";
    std::cin >> n;
    findPythagoreanTriples(n);
    return 0;
}

# 2
#include <iostream>
#include <vector>

void pascalTriangle(int n) {
    std::vector<std::vector<int>> triangle(n);

    for (int i = 0; i < n; i++) {
        triangle[i].resize(i + 1);
        triangle[i][0] = triangle[i][i] = 1;  

        for (int j = 1; j < i; j++) {
            triangle[i][j] = triangle[i-1][j-1] + triangle[i-1][j];
        }
    }

    for (const auto& row : triangle) {
        for (int num : row) {
            std::cout << num << " ";
        }
        std::cout << std::endl;
    }
}

int main() {
    int n;
    std::cout << "Enter n: ";
    std::cin >> n;
    pascalTriangle(n);
    return 0;
}
# 3
#include <iostream>
#include <vector>

void sieve(int n) {
    std::vector<bool> isPrime(n + 1, true);
    isPrime[0] = isPrime[1] = false;

    for (int i = 2; i * i <= n; i++) {
        if (isPrime[i]) {
            for (int j = i * i; j <= n; j += i) {
                isPrime[j] = false;
            }
        }
    }

    for (int i = 2; i <= n; i++) {
        if (isPrime[i]) {
            std::cout << i << " ";
        }
    }
    std::cout << std::endl;
}

int main() {
    int n = 1000;
    sieve(n);
    return 0;
}
# 4
#include <iostream>
#include <vector>

void primeFactorization(int n) {
    std::vector<int> factors;

    for (int i = 2; i <= n; i++) {
        while (n % i == 0) {
            factors.push_back(i);
            n /= i;
        }
    }

    for (int factor : factors) {
        std::cout << factor << " ";
    }
    std::cout << std::endl;
}

int main() {
    int n;
    std::cout << "Enter number: ";
    std::cin >> n;
    primeFactorization(n);
    return 0;
}

# 5
#include <iostream>
#include <cmath>

bool isPalindrome(int x) {
    int original = x;
    int reversed = 0;
    while (x > 0) {
        reversed = reversed * 10 + x % 10;
        x /= 10;
    }
    return original == reversed;
}

int main() {
    for (int i = 1; i < 100; i++) {
        if (isPalindrome(i)) {
            int square = i * i;
            if (isPalindrome(square)) {
                std::cout << i << " " << square << std::endl;
            }
        }
    }
    return 0;
}

# 6
#include <iostream>
#include <vector>

std::string numberToWords(int n) {
    std::vector<std::string> below20 = {"", "one", "two", "three", "four", "five", "six", "seven", "eight", "nine", "ten", "eleven", "twelve", "thirteen", "fourteen", "fifteen", "sixteen", "seventeen", "eighteen", "nineteen"};
    std::vector<std::string> tens = {"", "", "twenty", "thirty", "forty", "fifty", "sixty", "seventy", "eighty", "ninety"};
    std::vector<std::string> thousands = {"", "thousand"};

    if (n == 0) return "zero";

    std::string result = "";
    if (n >= 1000) {
        result += below20[n / 1000] + " thousand ";
        n %= 1000;
    }
    if (n >= 100) {
        result += below20[n / 100] + " hundred ";
        n %= 100;
    }
    if (n >= 20) {
        result += tens[n / 10] + " ";
        n %= 10;
    }
    if (n > 0) {
        result += below20[n];
    }

    return result;
}

int main() {
    int n;
    std::cout << "Enter number: ";
    std::cin >> n;
    std::cout << numberToWords(n) << std::endl;
    return 0;
}

# 7
#include <iostream>
#include <vector>

bool isPrime(int n) {
    if (n <= 1) return false;
    for (int i = 2; i * i <= n; i++) {
        if (n % i == 0) return false;
    }
    return true;
}

int main() {
    int n;
    std::cout << "Enter n: ";
    std::cin >> n;

    for (int i = n; i <= 2 * n; i++) {
        if (isPrime(i) && isPrime(i + 2)) {
            std::cout << i << " " << i + 2 << std::endl;
        }
    }

    return 0;
}

# 8
#include <iostream>
#include <string>
#include <sstream>
#include <vector>

void formatText(std::string text, int n) {
    std::istringstream stream(text);
    std::string line;
    std::string result;
    
    while (std::getline(stream, line)) {
        std::string formattedLine = "";
        std::istringstream words(line);
        std::string word;
        
        while (words >> word) {
            if (formattedLine.length() + word.length() + 1 <= n) {
                if (!formattedLine.empty()) formattedLine += " ";
                formattedLine += word;
            } else {
                result += formattedLine + "\n";
                formattedLine = word;
            }
        }
        
        if (!formattedLine.empty()) {
            result += formattedLine + "\n";
        }
    }

    std::cout << result;
}

int main() {
    std::string text = "Це приклад тексту. Ми будемо редагувати його, щоб кожен рядок не перевищував певної кількості символів.";
    int n;
    std::cout << "Enter width n > 50: ";
    std::cin >> n;
    formatText(text, n);
    return 0;
}

# 9
#include <iostream>
#include <string>
#include <bitset>
#include <sstream>

std::string encodeSteganography(const std::string& message) {
    std::string encodedMessage = "";
    for (char ch : message) {
        std::bitset<8> binary(ch);  // Перетворюємо символ у двійкове представлення
        std::string binStr = binary.to_string();
        
        for (char bit : binStr) {
            if (bit == '0') {
                encodedMessage += " ";
            } else {
                encodedMessage += "  ";
            }
        }
    }
    return encodedMessage;
}

std::string decodeSteganography(const std::string& encodedMessage) {
    std::string decodedMessage = "";
    std::string temp = "";
    int spaceCount = 0;
    
    for (char ch : encodedMessage) {
        if (ch == ' ') {
            spaceCount++;
            if (spaceCount == 2) {
                temp += '1';
                spaceCount = 0;
            } else if (spaceCount == 1) {
                temp += '0';
            }
        } else {
            if (!temp.empty()) {
                decodedMessage += char(std::bitset<8>(temp).to_ulong());
                temp = "";
            }
        }
    }

    if (!temp.empty()) {
        decodedMessage += char(std::bitset<8>(temp).to_ulong());
    }

    return decodedMessage;
}

int main() {
    std::string message = "Hello";
    std::string encoded = encodeSteganography(message);
    std::cout << "Encoded message: " << encoded << std::endl;
    
    std::string decoded = decodeSteganography(encoded);
    std::cout << "Decoded message: " << decoded << std::endl;

    return 0;
}

# 10
#include <iostream>
#include <vector>

bool isMagical(std::vector<int>& vec) {
    int sum = 0, prod = 1;
    for (int num : vec) {
        sum += num;
        prod *= num;
    }
    return sum == prod;
}

void findMagicalVectors(int N) {
    std::vector<int> vec(N, 1);
    while (true) {
        if (isMagical(vec)) {
            for (int num : vec) {
                std::cout << num << " ";
            }
            std::cout << std::endl;
        }

        int i = N - 1;
        while (i >= 0 && vec[i] == N) {
            i--;
        }
        
        if (i < 0) break;
        
        vec[i]++;
        for (int j = i + 1; j < N; j++) {
            vec[j] = 1;
        }
    }
}

int main() {
    int N;
    std::cout << "Enter N: ";
    std::cin >> N;
    findMagicalVectors(N);
    return 0;
}

# 11
#include <iostream>
#include <vector>
#include <cmath>

struct City {
    int x, y;
};

int calculateDistance(const City& a, const City& b) {
    return std::abs(a.x - b.x) + std::abs(a.y - b.y);
}

City findCapital(const std::vector<City>& cities) {
    int sumX = 0, sumY = 0;
    for (const City& city : cities) {
        sumX += city.x;
        sumY += city.y;
    }

    int capitalX = sumX / cities.size();
    int capitalY = sumY / cities.size();

    return {capitalX, capitalY};
}

int main() {
    std::vector<City> cities = {{1, 2}, {3, 4}, {5, 6}, {7, 8}};
    
    City capital = findCapital(cities);
    std::cout << "The coordinates of the capital are: (" 
              << capital.x << ", " << capital.y << ")\n";

    return 0;
}
