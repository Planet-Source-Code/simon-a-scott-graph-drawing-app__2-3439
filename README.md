<div align="center">

## Graph Drawing app


</div>

### Description

Shows how we can input data for 5 variables and generate a bar-graph and a pie-chart from this data. The code is designed to help people who may need to display info in a graphic form and to develop the code to suit their own needs.
 
### More Info
 
Needs to be compiled


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[Simon A Scott](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/simon-a-scott.md)
**Level**          |Intermediate
**User Rating**    |5.0 (10 globes from 2 users)
**Compatibility**  |Java \(JDK 1\.2\)
**Category**       |[Complete Applications](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/complete-applications__2-64.md)
**World**          |[Java](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/java.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/simon-a-scott-graph-drawing-app__2-3439/archive/master.zip)





### Source Code

```
import java.awt.*;
import java.awt.event.*;
import javax.swing.*;
public class DynamicGraph extends JFrame implements ActionListener {
 JButton button;
 int []bar = new int[5];
 float []flote = new float[5];
 String str = "", title="";
 String []barLabels = {"","","","",""};
 String []percent = {"","","","",""};
 JLabel []JLab = new JLabel[5];
 JTextField titletxt;
 JTextField []Text = new JTextField[5];
 JTextField []labeltxt = new JTextField[5];
 boolean pieChart;
public DynamicGraph() {
   super("Dynamic Graph");
   Container c  = getContentPane();
    JPanel panel = new JPanel(){
  public void paintComponent(Graphics g){
      Graphics2D g2 = (Graphics2D)g;
      g2.setColor(new Color(223,222,224));
      g2.fillRect(0,0,500,400);
      g2.setColor(Color.orange);
        if(pieChart) {
         g2.fillArc(30, 130, 220, 220, 90, -bar[0]);
         g2.fillRect(270, 170, 30, 20);
        }
        else g2.fillRect(30, 150, bar[0], 30);
      g2.setColor(Color.green);
        if(pieChart) {
         g2.fillArc(30, 130, 220, 220, 90-bar[0], -bar[1]);
         g2.fillRect(270, 210, 30, 20);
        }
        else g2.fillRect(30, 190, bar[1], 30);
      g2.setColor(Color.red);
        if(pieChart) {
         g2.fillArc(30, 130, 220, 220, 90-(bar[0]+bar[1]), -bar[2]);
         g2.fillRect(270, 250, 30, 20);
        }
        else g2.fillRect(30, 230, bar[2], 30);
      g2.setColor(Color.blue);
        if(pieChart) {
         g2.fillArc(30, 130, 220, 220, 90-(bar[0]+bar[1]+bar[2]), -bar[3]);
         g2.fillRect(270, 290, 30, 20);
        }
        else g2.fillRect(30, 270, bar[3], 30);
      g2.setColor(Color.yellow);
        if(pieChart) {
         g2.fillArc(30, 130, 220, 220, 90-(bar[0]+bar[1]+bar[2]+bar[3]), -bar[4]);
         g2.fillRect(270, 330, 30, 20);
        }
        else g2.fillRect(30, 310, bar[4], 30);
      g2.setColor(Color.black);
      g2.setFont(new Font("Arial", Font.BOLD, 18));
        if(pieChart) g2.drawString(title, 220, 142);
        else g2.drawString(title, 50, 132);
      g2.setFont(new Font("Arial", Font.PLAIN,16));
      int temp=0;
        if(pieChart) temp = 185;
        else temp = 172;
         for(int j=0; j <5; j++) {
          if(pieChart) g2.drawString(barLabels[j]+percent[j], 305, temp);
          else g2.drawString(barLabels[j]+percent[j], bar[j]+40, temp);
          temp += 40;
         }
        if(!pieChart){
         g2.drawLine(30, 130, 30, 350);
         g2.drawLine(30, 345, 430, 345);
         g2.drawLine(210, 345, 210, 350);
         g2.drawLine(390, 345, 390, 350);
         g2.setFont(new Font("Arial", Font.PLAIN,12));
         g2.drawString("0%", 26, 362);
         g2.drawString("25%", 113, 362);
         g2.drawString("50%", 200, 362);
         g2.drawString("75%", 287, 362);
         g2.drawString("100%", 380, 362);
        }
super.paintComponent(g2);
  }
  };
  panel.setOpaque(false);
   panel.setLayout(new FlowLayout() );
   button = new JButton("Draw 1");
   JLabel jLab = new JLabel("<html><font face='Arial'>Enter graph title here, then labels and<br>number values and press the button</font></html>");
   titletxt = new JTextField(18);
   panel.add(jLab);
   panel.add(titletxt);
   JLabel addNums = new JLabel("Labels: ");
   panel.add(addNums);
     for (int j=0; j<5; j++){
       str = Integer.toString(j+1);
       JLab[j] = new JLabel(str);
       labeltxt[j] = new JTextField(6);
       panel.add(JLab[j]);
       panel.add(labeltxt[j]);
     }
   button.addActionListener(this);
   JLabel labellers = new JLabel("Numbers");
   panel.add(labellers);
     for (int k=0; k<5; k++){
       str = Integer.toString(k+1);
       JLab[k] = new JLabel("  "+str+" ");
       Text[k] = new JTextField(3);
       panel.add(JLab[k]);
       panel.add(Text[k]);
     }
   panel.add(button);
   c.add(panel);
 }
public void actionPerformed(ActionEvent e) {
  String command = e.getActionCommand();
   if(command.equals("Draw 1")){
    button.setText("Draw 2");
    pieChart=false;
    try {
    title = titletxt.getText();
     if(title.length() <1)title ="No title submitted";
     int temp =0;
     java.text.DecimalFormat df = new java.text.DecimalFormat("#0.#");
      for (int j=0; j<5; j++){
       flote[j] = Float.parseFloat(Text[j].getText());
       temp += (int)((flote[j]) +0.5);
      }
      for (int k=0; k<5; k++){
       bar[k] = (int)(((flote[k]/temp) * 360)+0.5);
       barLabels[k] = labeltxt[k].getText();
       flote[k] = (flote[k]/temp) *100;
       percent[k] = ": "+df.format(flote[k])+"%";
      }
    }
    catch(Exception message){
      title = "Oops! Complete all fields, enter numbers only";
    }
   }
   if(command.equals("Draw 2")){
    button.setText("Draw 1");
    pieChart=true;
   }
  repaint();
}
 public static void main(String[] args) {
  DynamicGraph frame = new DynamicGraph();
  frame.setSize(500,400);
  frame.setLocation(200, 200);
  frame.setResizable(false);
  frame.setDefaultCloseOperation( EXIT_ON_CLOSE );
  frame.setVisible(true);
 }
}
```

