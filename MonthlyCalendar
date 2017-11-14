package monthlycalendar;

import java.util.*;

import java.awt.*;

import java.awt.event.*;

import javax.swing.*;

import javax.swing.event.*;

import javax.swing.table.DefaultTableModel;


public class MonthlyCalendar extends JFrame implements ActionListener,CaretListener {
	
	public JTextField text;
	public JComboBox<String>combox_month,combox_day;
	public Message jdialog;
	public DefaultTableModel tableModel;
	
	public MonthlyCalendar() {
		super("日期");
		this.setLayout(new BorderLayout());
		Dimension dim = getToolkit().getScreenSize();
		this.setBounds(dim.width/4,dim.height/8,dim.width/2,dim.height/2);
		this.setDefaultCloseOperation(EXIT_ON_CLOSE);
		
		String[] str = {"年 ","月 ","日"};
		String month[] = new String[12];
		String day[] = new String[31];
		for (int i = 0; i < 12; i++) {
			month[i]=(new Integer(i+1)).toString();
		}
		for (int j = 0; j < 31; j++) {
			day[j] = (new Integer(j+1).toString());
		}
		
		JPanel jpanel = new JPanel();
		this.getContentPane().add(jpanel,"North");
		
		jpanel.add(this.text = new JTextField("2017",5));
		this.text.addCaretListener(this);
		jpanel.add(new JLabel(str[0]));
		jpanel.add(this.combox_month = new JComboBox<String>(month));
		this.combox_month.addActionListener(this);
		jpanel.add(new JLabel(str[1]));
		jpanel.add(this.combox_day = new JComboBox<String>(day));
		jpanel.add(new JLabel(str[2]));
		
		String titles[] = {"日","一","二","三","四","五","六"};
		this.tableModel = new DefaultTableModel(titles,0);
		JTable table = new JTable(this.tableModel);
//		JPanel tablepane = new JPanel();
//		tablepane.add(table);
		this.getContentPane().add(new JScrollPane(table));
		setTable(Integer.parseInt(text.getText()),this.combox_month.getSelectedIndex()+1);
		this.setVisible(true);
		jdialog = new Message();
	}
	
	@Override
	public void actionPerformed(ActionEvent ev) {
		int month = this.combox_month.getSelectedIndex()+1;
		int year = Integer.parseInt(text.getText());
		setDay(year,month);
		setTable(year,month);
//		GregorianCalendar calendar = new GregorianCalendar(year,month,1);
//		int week = calendar.get(Calendar.DAY_OF_WEEK)-1;
//		int count = 1;
//		for (int j = 0;j<7;j++) {
//			for(;week<7;week++) {
//				if(count<=monthLength(year,month)) {
//					this.tableModel.setValueAt(count, j, week);
//					count++;
//				}
//			}
//			week = 0;
//		}
	}
	
	public void setTable(int year,int month) {
		
		this.tableModel.setRowCount(6);
		GregorianCalendar calendar = new GregorianCalendar(year,month-1,1);
		int week = calendar.get(Calendar.DAY_OF_WEEK)-1;
		int count = 1;
		for(int m = 0; m < 6; m++) {
			for(int n = 0; n < 7; n++)
				this.tableModel.setValueAt("", m, n);
		}
		for (int j = 0; j < 6; j++) {
			for(; week < 7; week++) {
				if(count<=monthLength(year,month)) {
					this.tableModel.setValueAt(count, j, week);
					count++;
				} else {
					break;
				}
			}
			week = 0;
		}
	}
	
	public void setDay(int year,int month) {
		int n = monthLength(year,month);
//	int days = MyDate.daysOfMonth(year,month);
		this.combox_day.removeAllItems();
		for (int k=0;k<n;k++) {
			this.combox_day.addItem((new Integer(k+1)).toString());
		}
	}
	
	public int monthLength(int year,int month) {
		int d[] = {1,3,5,7,8,10,12};
		int m[] = {4,6,9,11};
		for (int i :d) {
			if (i==month) {
				return 31;
			}
		}
		for (int j:m) {
			if (j==month) {
				return 30;
			}
		}
		if (month == 2) {
			if(isLeapYear(year)) {
				return 29;
			} else {
				return 28;
			}
		}
		return 0;
	}
	
	public boolean isLeapYear(int year) {
		return year%4==0&&(year%100!=0||year%400==0);
	}

	@Override
	public void caretUpdate(CaretEvent ev) {
		try {
			int i = Integer.parseInt(text.getText());
			setTable(i,this.combox_month.getSelectedIndex()+1);
		} catch(NumberFormatException nfex) {
			jdialog.show(text.getText()+"输入错误！");
		} finally {}
	}
	
	public static void main(String[] args) {
		// TODO Auto-generated method stub
		new MonthlyCalendar();
	}

	private class Message extends JDialog {
		private JLabel label;
		
		public Message() {
			super(MonthlyCalendar.this,"提示",true);
			this.setSize(200,80);
			label = new JLabel("",JLabel.CENTER);
			this.getContentPane().add(label);
			this.setDefaultCloseOperation(HIDE_ON_CLOSE);
		}
		
		public void show(String message) {
			label.setText(message);
			this.setLocation(MonthlyCalendar.this.getX()+350,MonthlyCalendar.this.getY()+100);
			this.setVisible(true);
		}
	}

}
