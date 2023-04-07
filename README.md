# Time_table.java
import java.awt.*;
import java.awt.event.*;
import javax.swing.*;

public class TimeTableApplet extends JApplet {
    private static final long serialVersionUID = 1L;
    private JTextField[][] timetable;
    private String[] days = { "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday" };
    private String[] periods = { "1", "2", "3", "4", "5", "6", "7", "8", "9", "10" };
    
    public void init() {
        createGUI();
    }
    
    private void createGUI() {
        JPanel panel = new JPanel(new BorderLayout());
        JPanel tablePanel = new JPanel(new GridLayout(periods.length + 1, days.length + 1));
        
        timetable = new JTextField[periods.length][days.length];
        
        // Create table headers
        JLabel blankLabel = new JLabel("");
        tablePanel.add(blankLabel);
        for (int i = 0; i < days.length; i++) {
            JLabel dayLabel = new JLabel(days[i]);
            tablePanel.add(dayLabel);
        }
        
        // Create timetable
        for (int i = 0; i < periods.length; i++) {
            JLabel periodLabel = new JLabel(periods[i]);
            tablePanel.add(periodLabel);
            
            for (int j = 0; j < days.length; j++) {
                JTextField field = new JTextField(10);
                timetable[i][j] = field;
                tablePanel.add(field);
            }
        }
        
        panel.add(tablePanel, BorderLayout.CENTER);
        
        // Add save button
        JButton saveButton = new JButton("Save");
        saveButton.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                saveTimetable();
            }
        });
        
        panel.add(saveButton, BorderLayout.SOUTH);
        
        getContentPane().add(panel);
    }
    
    private void saveTimetable() {
        // Get timetable data and save to file/database
        for (int i = 0; i < periods.length; i++) {
            for (int j = 0; j < days.length; j++) {
                String data = timetable[i][j].getText();
                System.out.println("Period: " + periods[i] + ", Day: " + days[j] + ", Data: " + data);
            }
        }
    }
    
    public static void main(String[] args) {
        JFrame frame = new JFrame("Timetable Applet");
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        JApplet applet = new TimeTableApplet();
        applet.init();
        frame.getContentPane().add(applet);
        frame.pack();
        frame.setVisible(true);
    }
}
