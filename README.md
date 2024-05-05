#include <iostream>
#include <cstdlib>
#include <ctime>
#include <vector>
#include <string>
#include <sstream>

// 生成随机数
int generateRandomNumber(int maxNum) {
    return rand() % maxNum + 1;
}

// 生成随机运算符
char generateRandomOperator(std::vector<char> operators) {
    int index = rand() % operators.size();
    return operators[index];
}

// 生成四则运算表达式
std::string generateExpression(int maxNum, std::vector<char> operators, bool withBrackets, bool withDecimal) {
    int num1 = generateRandomNumber(maxNum);
    int num2 = generateRandomNumber(maxNum);
    char op = generateRandomOperator(operators);

    // 添加括号
    if (withBrackets && rand() % 2 == 0) {
        return "(" + std::to_string(num1) + " " + op + " " + std::to_string(num2) + ")";
    }

    // 生成小数
    if (withDecimal && rand() % 2 == 0) {
        float result = static_cast<float>(num1) + static_cast<float>(num2) / 10;
        std::ostringstream ss;
        ss << result;
        return ss.str();
    }

    return std::to_string(num1) + " " + op + " " + std::to_string(num2);
}

int main() {
    srand(time(0));

    int numQuestions;
    char operatorChoice;
    int maxNumber;
    bool withBrackets;
    bool withDecimal;

    std::cout << "Enter number of questions: ";
    std::cin >> numQuestions;

    std::cout << "Enter operator choice (+, -, *, /): ";
    std::cin >> operatorChoice;

    std::vector<char> operators;
    operators.push_back(operatorChoice);

    std::cout << "Enter max number: ";
    std::cin >> maxNumber;

    std::cout << "Include brackets? (1 for yes, 0 for no): ";
    std::cin >> withBrackets;

    std::cout << "Include decimals? (1 for yes, 0 for no): ";
    std::cin >> withDecimal;

    for (int i = 0; i < numQuestions; i++) {
        std::string expression = generateExpression(maxNumber, operators, withBrackets, withDecimal);
        std::cout << expression << std::endl;
    }

    return 0;
}
