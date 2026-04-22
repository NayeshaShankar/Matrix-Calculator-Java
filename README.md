[Matrix Calculator in Java using swing]

```
package matrixxx;

import javax.swing.*;
import java.awt.*;

public class Matrixxx {

    static JFrame frame;
    static JTextField rowsField, colsField;
    static JPanel panelA, panelB, resultPanel;
    static JTextField[][] matrixA, matrixB;

    public static void main(String[] args) {

        frame = new JFrame("Matrix Calculator");
        frame.setSize(700, 600);
        frame.setLayout(new BorderLayout());

        // 🔹 Top Panel
        JPanel top = new JPanel();
        top.add(new JLabel("Rows:"));
        rowsField = new JTextField(5);
        top.add(rowsField);

        top.add(new JLabel("Cols:"));
        colsField = new JTextField(5);
        top.add(colsField);

        JButton createBtn = new JButton("Create");
        top.add(createBtn);

        frame.add(top, BorderLayout.NORTH);

        // 🔹 Center Panel with Titles
        JPanel center = new JPanel(new GridLayout(1, 3));

        panelA = new JPanel();
        panelB = new JPanel();
        resultPanel = new JPanel();

        JPanel wrapperA = new JPanel(new BorderLayout());
        wrapperA.add(new JLabel("Matrix A", SwingConstants.CENTER), BorderLayout.NORTH);
        wrapperA.add(panelA, BorderLayout.CENTER);

        JPanel wrapperB = new JPanel(new BorderLayout());
        wrapperB.add(new JLabel("Matrix B", SwingConstants.CENTER), BorderLayout.NORTH);
        wrapperB.add(panelB, BorderLayout.CENTER);

        JPanel wrapperR = new JPanel(new BorderLayout());
        wrapperR.add(new JLabel("Result", SwingConstants.CENTER), BorderLayout.NORTH);
        wrapperR.add(resultPanel, BorderLayout.CENTER);

        center.add(wrapperA);
        center.add(wrapperB);
        center.add(wrapperR);

        frame.add(center, BorderLayout.CENTER);

        // 🔹 Bottom Panel
        JPanel bottom = new JPanel();

        JButton addBtn = new JButton("Add");
        JButton subBtn = new JButton("Subtract");
        JButton mulBtn = new JButton("Multiply");
        JButton clearBtn = new JButton("Clear");

        bottom.add(addBtn);
        bottom.add(subBtn);
        bottom.add(mulBtn);
        bottom.add(clearBtn);

        frame.add(bottom, BorderLayout.SOUTH);

        // 🔹 Create Matrices
        createBtn.addActionListener(e -> {
            int rows = Integer.parseInt(rowsField.getText());
            int cols = Integer.parseInt(colsField.getText());

            panelA.removeAll();
            panelB.removeAll();

            panelA.setLayout(new GridLayout(rows, cols, 5, 5));
            panelB.setLayout(new GridLayout(rows, cols, 5, 5));

            matrixA = new JTextField[rows][cols];
            matrixB = new JTextField[rows][cols];

            for (int i = 0; i < rows; i++) {
                for (int j = 0; j < cols; j++) {
                    matrixA[i][j] = new JTextField(3);
                    matrixB[i][j] = new JTextField(3);

                    panelA.add(matrixA[i][j]);
                    panelB.add(matrixB[i][j]);
                }
            }

            panelA.revalidate();
            panelB.revalidate();
        });

        // 🔹 Add
        addBtn.addActionListener(e -> calculate("+"));

        // 🔹 Subtract
        subBtn.addActionListener(e -> calculate("-"));

        // 🔹 Multiply
        mulBtn.addActionListener(e -> calculate("*"));

        // 🔹 Clear Button
        clearBtn.addActionListener(e -> {
            panelA.removeAll();
            panelB.removeAll();
            resultPanel.removeAll();

            rowsField.setText("");
            colsField.setText("");

            frame.revalidate();
            frame.repaint();
        });

        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        frame.setVisible(true);
    }

    // 🔹 Calculation
    static void calculate(String op) {
        int rows = matrixA.length;
        int cols = matrixA[0].length;

        int[][] result = new int[rows][cols];

        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < cols; j++) {

                if (op.equals("*")) {
                    for (int k = 0; k < cols; k++) {
                        int a = Integer.parseInt(matrixA[i][k].getText());
                        int b = Integer.parseInt(matrixB[k][j].getText());
                        result[i][j] += a * b;
                    }
                } else {
                    int a = Integer.parseInt(matrixA[i][j].getText());
                    int b = Integer.parseInt(matrixB[i][j].getText());

                    result[i][j] = op.equals("+") ? a + b : a - b;
                }
            }
        }

        showResult(result, rows, cols);
    }

    // 🔹 Show Result
    static void showResult(int[][] result, int rows, int cols) {

        resultPanel.removeAll();
        resultPanel.setLayout(new GridLayout(rows, cols, 5, 5));

        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < cols; j++) {
                JTextField field = new JTextField(String.valueOf(result[i][j]));
                field.setEditable(false);
                resultPanel.add(field);
            }
        }

        resultPanel.revalidate();
        resultPanel.repaint();
    }
}

```

<img width="868" height="742" alt="{DD817497-86F8-4EA1-84F5-4CEDAE7B29F9}" src="https://github.com/user-attachments/assets/bc02b37f-29a0-4718-a9ff-12047e43ee75" />
