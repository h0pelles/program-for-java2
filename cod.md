import java.io.BufferedWriter;
import java.io.FileWriter;
import java.io.IOException;

public class SpiralArray {

    public static void main(String[] args) {
        int m = 5; 
        int n = 5; 
        
        int[][] spiral = generateSpiralArray(m, n);
        printSpiralArray(spiral);
        saveSpiralArrayToFile(spiral, "spiral_array.txt");
    }

    public static int[][] generateSpiralArray(int m, int n) {
        int[][] spiral = new int[m][n];

        int layer = 0;
        int number = 1;

        while (layer <= Math.min(m, n) / 2) {
            
            for (int i = layer; i < n - layer; i++) {
                spiral[layer][i] = number;
                number++;
            }

            for (int i = layer + 1; i < m - layer; i++) {
                spiral[i][n - 1 - layer] = number;
                number++;
            }

            for (int i = n - 2 - layer; i >= layer; i--) {
                spiral[m - 1 - layer][i] = number;
                number++;
            }

            for (int i = m - 2 - layer; i > layer; i--) {
                spiral[i][layer] = number;
                number++;
            }

            layer++;
        }

        return spiral;
    }

    
    public static void printSpiralArray(int[][] spiral) {
        for (int i = 0; i < spiral.length; i++) {
            for (int j = 0; j < spiral[0].length; j++) {
                System.out.print(spiral[i][j] + "\t");
            }
            System.out.println();
        }
    }

    
    public static void saveSpiralArrayToFile(int[][] spiral, String filename) {
        try (BufferedWriter writer = new BufferedWriter(new FileWriter(filename))) {
            for (int i = 0; i < spiral.length; i++) {
                for (int j = 0; j < spiral[0].length; j++) {
                    writer.write(spiral[i][j] + "\t");
                }
                writer.newLine();
            }
            System.out.println("Спиральный массив успешно сохранен в файл: " + filename);
        } catch (IOException e) {
            System.err.println("Ошибка при записи в файл: " + e.getMessage());
        }
    }
}
