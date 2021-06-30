import javax.swing.*;
import javax.swing.border.LineBorder;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.text.DecimalFormat;


public class Calculator extends JFrame implements ActionListener {
    JFrame frame;
    JPanel mainPanel, buttonsPanel;
    JTextField display;
    JButton bC, bPlus_Minus, b100, bImp, bad, bInm, bsc, beq, bvirgula, bsqrt;
    JButton[] nrButton = new JButton[10];
    double a = 0, b = 0, result = 0;
    String operator = "";

    Calculator() {
        initComponent();
    }


    public void initComponent() {
        frame = new JFrame("Calculator");
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        frame.setSize(300, 400);
        frame.setBackground(Color.BLACK);

        // mainPanel = new JPanel(new GridLayout(8, 0));
        mainPanel = new JPanel();
        mainPanel.setBackground(Color.BLACK);
        display = new JTextField("", 10);
        display.setEditable(false);


        display.setHorizontalAlignment(JTextField.RIGHT);
        display.setFont(new Font("Times New Roman", Font.PLAIN, 36));
        display.setForeground(Color.WHITE);
        display.setBackground(Color.BLACK);
        display.setBorder(new LineBorder(Color.BLACK));

        bC = new JButton("C");
        bPlus_Minus = new JButton("+/-");
        b100 = new JButton("%");
        bImp = new JButton("/");
        bInm = new JButton("x");
        bsc = new JButton("-");
        bad = new JButton("+");
        beq = new JButton("=");
        bvirgula = new JButton(".");

        for (int i = 0; i <= 9; i++) {
            nrButton[i] = new JButton(i + "");
            nrButton[i].setBackground(Color.DARK_GRAY);
            nrButton[i].setForeground(Color.WHITE);
            nrButton[i].setBorder(new LineBorder(Color.BLACK));
        }

        bsqrt = new JButton("sqrt");
        nrButton[1].setPreferredSize(new Dimension(60, 50)); //daca pun la una, dupa se pun la toate

        bvirgula.setBackground(Color.DARK_GRAY);
        bvirgula.setForeground(Color.WHITE);
        bvirgula.setBorder(new LineBorder(Color.BLACK));
        beq.setBackground(Color.DARK_GRAY);
        beq.setForeground(Color.WHITE);
        beq.setBorder(new LineBorder(Color.BLACK));

        bC.setBackground(Color.LIGHT_GRAY);
        bC.setForeground(Color.BLACK);
        bC.setBorder(new LineBorder(Color.BLACK));
        bPlus_Minus.setBackground(Color.LIGHT_GRAY);
        bPlus_Minus.setForeground(Color.BLACK);
        bPlus_Minus.setBorder(new LineBorder(Color.BLACK));
        b100.setBackground(Color.LIGHT_GRAY);
        b100.setForeground(Color.BLACK);
        b100.setBorder(new LineBorder(Color.BLACK));


        Color colorOrange = new Color(255, 152, 23);
        bImp.setBackground(colorOrange);
        bImp.setForeground(Color.WHITE);
        bImp.setBorder(new LineBorder(Color.BLACK));
        bInm.setBackground(colorOrange);
        bInm.setForeground(Color.WHITE);
        bInm.setBorder(new LineBorder(Color.BLACK));
        bad.setBackground(colorOrange);
        bad.setForeground(Color.WHITE);
        bad.setBorder(new LineBorder(Color.BLACK));
        bsqrt.setBackground(colorOrange);
        bsqrt.setForeground(Color.WHITE);
        bsqrt.setBorder(new LineBorder(Color.BLACK));
        bsc.setBackground(colorOrange);
        bsc.setForeground(Color.WHITE);
        bsc.setBorder(new LineBorder(Color.BLACK));

//display.addActionListener(this);
        bC.addActionListener(this);
        bPlus_Minus.addActionListener(this);
        b100.addActionListener(this);
        bImp.addActionListener(this);
        bInm.addActionListener(this);
        bsc.addActionListener(this);
        bad.addActionListener(this);
        beq.addActionListener(this);
        bvirgula.addActionListener(this);
        bsqrt.addActionListener(this);
        for (int i = 0; i <= 9; i++) {
            nrButton[i].addActionListener(this);
        }

        buttonsPanel = new JPanel(new GridLayout(5, 4, 10, 10));
        buttonsPanel.setBackground(Color.BLACK);

        buttonsPanel.add(bC);
        buttonsPanel.add(bPlus_Minus);
        buttonsPanel.add(b100);
        buttonsPanel.add(bImp);
        buttonsPanel.add(nrButton[7]);
        buttonsPanel.add(nrButton[8]);
        buttonsPanel.add(nrButton[9]);
        buttonsPanel.add(bInm);
        buttonsPanel.add(nrButton[4]);
        buttonsPanel.add(nrButton[5]);
        buttonsPanel.add(nrButton[6]);
        buttonsPanel.add(bsc);
        buttonsPanel.add(nrButton[1]);
        buttonsPanel.add(nrButton[2]);
        buttonsPanel.add(nrButton[3]);
        buttonsPanel.add(bad);
        buttonsPanel.add(nrButton[0]);
        //buttonsPanel.add(b01);
        buttonsPanel.add(bvirgula);
        buttonsPanel.add(beq);
        buttonsPanel.add(bsqrt);

        mainPanel.add(display);
        mainPanel.add(buttonsPanel);

        frame.setContentPane(mainPanel);
        frame.setVisible(true);
    }


    public void actionPerformed(ActionEvent e) {
        DecimalFormat numberFormat = new DecimalFormat("#.######");
        for (int i = 0; i <= 9; i++) {
            if (e.getSource() == nrButton[i])
                display.setText(display.getText().concat("" + i));
        }
        if (e.getSource() == bvirgula)
            display.setText(display.getText().concat("."));
        if (e.getSource() == bPlus_Minus) {
            String x = "-";
            display.setText(x.concat(display.getText()));
        }
        if (e.getSource() == bsqrt) {
         /*
            double y = Double.parseDouble(display.getText());
            if (y == Math.sqrt(y) * Math.sqrt(y))
                display.setText("" + Math.round(Math.sqrt(y)));
            else {
                String strDouble = String.format("%.5f", Math.sqrt(y));
                display.setText(strDouble);
            }
          */
            double y = Double.parseDouble(display.getText());
            display.setText("" + numberFormat.format(Math.sqrt(y)));
        }
        if (e.getSource() == b100) {
            double z = Double.parseDouble(display.getText());
            display.setText("" + z / 100);
        }
        if (e.getSource() == bad) {
            a = Double.parseDouble(display.getText());
            operator = "+";
            display.setText("");
        }
        if (e.getSource() == bsc) {
            a = Double.parseDouble(display.getText());
            operator = "-";
            display.setText("");
        }
        if (e.getSource() == bInm) {
            a = Double.parseDouble(display.getText());
            operator = "*";
            display.setText("");
        }
        if (e.getSource() == bImp) {
            a = Double.parseDouble(display.getText());
            operator = "/";
            display.setText("");
        }


        if (e.getSource() == beq) {
            b = Double.parseDouble(display.getText());
            switch (operator) {
                case "+":
                    result = a + b;
                    break;
                case "-":
                    result = a - b;
                    break;
                case "*":
                    result = a * b;
                    break;
                case "/":
                    result = a / b;
                    break;
                default:
                    result = 0;
            }
            display.setText("" + numberFormat.format(result));
        }
        if (e.getSource() == bC)
            display.setText("");

    }

    public static void main(String[] args) {
        new Calculator();
    }

}



