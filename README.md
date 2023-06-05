# assignmentcpp
# cpp code 

#include <iostream>
#include <vector>
#include <cmath>

std::vector<int> findMaxNetworkQualityCoordinate(std::vector<std::vector<int>>& towers, int radius) {
    int maxQuality = 0;
    std::vector<int> maxCoordinate = {0, 0};

    for (const auto& tower : towers) {
        int xi = tower[0];
        int yi = tower[1];
        int qi = tower[2];

        int distance = std::sqrt(std::pow(maxCoordinate[0] - xi, 2) + std::pow(maxCoordinate[1] - yi, 2));

        if (distance <= radius) {
            int signalQuality = std::floor(qi / (1 + distance));
            int totalQuality = maxQuality + signalQuality;

            if (totalQuality > maxQuality || (totalQuality == maxQuality && maxCoordinate > tower)) {
                maxQuality = totalQuality;
                maxCoordinate = tower;
            }
        }
    }

    return maxCoordinate;
}

int main() {
    std::vector<std::vector<int>> towers = {{1, 2, 5}, {2, 1, 7}, {3, 1, 9}};
    int radius = 2;

    std::vector<int> maxNetworkQualityCoordinate = findMaxNetworkQualityCoordinate(towers, radius);

    std::cout << "Max Network Quality Coordinate: [" << maxNetworkQualityCoordinate[0] << ", " << maxNetworkQualityCoordinate[1] << "]" << std::endl;

    return 0;
}
