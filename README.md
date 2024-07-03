In this time I made a way to add pepperoni on pizza


package pizzaplace;

import java.awt.*;
import javax.swing.JPanel;
import javax.swing.JFrame;
import java.awt.event.*;

class MyCanvas extends JPanel implements ActionListener {
    Label myPrompt1, myPrompt2;
    TextField value1, value2;
    Button addButton, addOvalButton;
    int ovalWidth = 300;
    int ovalHeight = 300;
    boolean drawOval = false;
    int numPepperoni = 1;  // Default number of pepperoni

    public MyCanvas() {
        init();
    }

    public void paint(Graphics g) {
        super.paint(g);
        int width = getWidth();
        int height = getHeight();
        int x = (width - ovalWidth) / 2;
        int y = (height - ovalHeight) / 2;
        g.setColor(Color.yellow);
        g.fillOval(x, y, ovalWidth, ovalHeight);

        if (drawOval) {
            g.setColor(Color.red);
            int pepperoniWidth = ovalWidth / 10;
            int pepperoniHeight = ovalHeight / 10;

            for (int i = 0; i < numPepperoni; i++) {
                double angle = 2 * Math.PI * i / numPepperoni;
                int pepperoniX = (int) (x + ovalWidth / 2 + (ovalWidth / 3 * Math.cos(angle)) - pepperoniWidth / 2);
                int pepperoniY = (int) (y + ovalHeight / 2 + (ovalHeight / 3 * Math.sin(angle)) - pepperoniHeight / 2);
                g.fillOval(pepperoniX, pepperoniY, pepperoniWidth, pepperoniHeight);
            }
        }
    }

    public void init() {
        myPrompt1 = new Label("Enter pizza size:");
        value1 = new TextField(10);
        myPrompt2 = new Label("Enter number of pepperoni:");
        value2 = new TextField(10);
        addButton = new Button("Change Size");
        addOvalButton = new Button("Add pepperoni");

        add(myPrompt1);
        add(value1);
        add(myPrompt2);
        add(value2);
        add(addButton);
        add(addOvalButton);

        addButton.addActionListener(this);
        addOvalButton.addActionListener(this);
    }

    public void actionPerformed(ActionEvent e) {
        if (e.getSource() == addButton) {
            int newSize = Integer.parseInt(value1.getText());
            if (newSize > 0) {
                ovalWidth = newSize;
                ovalHeight = newSize;
                repaint();
            }
        } else if (e.getSource() == addOvalButton) {
            drawOval = true;
            numPepperoni = Integer.parseInt(value2.getText());
            repaint();
        }
    }
}

public class pizza {
    public static void main(String[] a) {
        JFrame window = new JFrame();
        window.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        window.setBounds(30, 30, 600, 600);
        window.getContentPane().add(new MyCanvas());
        window.setVisible(true);
    }
}
