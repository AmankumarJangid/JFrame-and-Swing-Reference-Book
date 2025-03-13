# JFrame-and-Swing-Reference-Book

# Java Swing Components Reference Guide

This comprehensive guide covers all major Swing components, their purposes, and basic usage examples.

## Basic Containers

### JFrame
The main application window with title bar, borders, and control buttons.
```java
JFrame frame = new JFrame("Application Title");
frame.setSize(800, 600);
frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
frame.setVisible(true);
```

### JPanel
A general-purpose container for organizing and grouping components.
```java
JPanel panel = new JPanel();
panel.setLayout(new FlowLayout());
frame.add(panel);
```

### JDialog
A secondary window for interactions like alerts or input forms.
```java
JDialog dialog = new JDialog(parentFrame, "Dialog Title", true); // modal dialog
dialog.setSize(400, 300);
dialog.setLocationRelativeTo(parentFrame);
```

### JInternalFrame
A JFrame-like component that lives inside a JDesktopPane for MDI applications.
```java
JInternalFrame internalFrame = new JInternalFrame("Document", true, true, true, true);
internalFrame.setSize(300, 200);
internalFrame.setVisible(true);
desktopPane.add(internalFrame);
```

## Basic Controls

### JButton
A standard clickable button.
```java
JButton button = new JButton("Click Me");
button.addActionListener(e -> System.out.println("Button clicked"));
```

### JLabel
Displays text or images.
```java
JLabel label = new JLabel("Text Label");
JLabel imageLabel = new JLabel(new ImageIcon("image.png"));
```

### JTextField
Single-line text input field.
```java
JTextField textField = new JTextField(20); // 20 columns wide
textField.setText("Default text");
String userInput = textField.getText();
```

### JPasswordField
Single-line masked text field for password entry.
```java
JPasswordField passwordField = new JPasswordField(20);
char[] password = passwordField.getPassword(); // More secure than getText()
```

### JTextArea
Multi-line text input and display area.
```java
JTextArea textArea = new JTextArea(10, 40); // 10 rows, 40 columns
textArea.setLineWrap(true);
textArea.setWrapStyleWord(true);
```

### JEditorPane
Displays formatted text including HTML.
```java
JEditorPane editorPane = new JEditorPane("text/html", "<html><body>HTML content</body></html>");
```

### JCheckBox
Toggle button with checked/unchecked states.
```java
JCheckBox checkBox = new JCheckBox("Enable feature");
checkBox.setSelected(true);
boolean isEnabled = checkBox.isSelected();
```

### JRadioButton
Option button, typically used in groups where only one can be selected.
```java
JRadioButton option1 = new JRadioButton("Option 1");
JRadioButton option2 = new JRadioButton("Option 2");
ButtonGroup group = new ButtonGroup(); // Ensures mutual exclusivity
group.add(option1);
group.add(option2);
```

### JToggleButton
Button that maintains selected/deselected state.
```java
JToggleButton toggleButton = new JToggleButton("Toggle");
toggleButton.addActionListener(e -> System.out.println("State: " + toggleButton.isSelected()));
```

## Selection Components

### JComboBox
Drop-down list for selecting one item from many.
```java
String[] options = {"Small", "Medium", "Large"};
JComboBox<String> comboBox = new JComboBox<>(options);
comboBox.setSelectedIndex(1); // Select "Medium"
String selected = (String)comboBox.getSelectedItem();
```

### JList
Displays a list of items for selection (single or multiple).
```java
String[] items = {"Item 1", "Item 2", "Item 3"};
JList<String> list = new JList<>(items);
list.setSelectionMode(ListSelectionModel.SINGLE_SELECTION);
list.addListSelectionListener(e -> {
    if (!e.getValueIsAdjusting()) {
        System.out.println("Selected: " + list.getSelectedValue());
    }
});
```

### JSpinner
Allows selecting a number or item from a sequence.
```java
SpinnerNumberModel model = new SpinnerNumberModel(5, 0, 10, 1); // initial, min, max, step
JSpinner spinner = new JSpinner(model);
int value = (Integer)spinner.getValue();
```

### JSlider
Allows selecting a value by dragging a slider knob.
```java
JSlider slider = new JSlider(JSlider.HORIZONTAL, 0, 100, 50); // orientation, min, max, initial
slider.setMajorTickSpacing(20);
slider.setMinorTickSpacing(5);
slider.setPaintTicks(true);
slider.setPaintLabels(true);
```

## Menu Components

### JMenuBar
The main container for menus.
```java
JMenuBar menuBar = new JMenuBar();
frame.setJMenuBar(menuBar);
```

### JMenu
A drop-down menu.
```java
JMenu fileMenu = new JMenu("File");
menuBar.add(fileMenu);
```

### JMenuItem
A selectable option in a menu.
```java
JMenuItem openItem = new JMenuItem("Open");
openItem.addActionListener(e -> System.out.println("Open selected"));
fileMenu.add(openItem);
```

### JCheckBoxMenuItem
A menu item with a checkbox.
```java
JCheckBoxMenuItem viewStatusBar = new JCheckBoxMenuItem("Show Status Bar");
viewStatusBar.setSelected(true);
```

### JRadioButtonMenuItem
A menu item with a radio button.
```java
JRadioButtonMenuItem sortAsc = new JRadioButtonMenuItem("Sort Ascending");
JRadioButtonMenuItem sortDesc = new JRadioButtonMenuItem("Sort Descending");
ButtonGroup sortGroup = new ButtonGroup();
sortGroup.add(sortAsc);
sortGroup.add(sortDesc);
```

### JPopupMenu
A context menu that appears at a specific position.
```java
JPopupMenu popupMenu = new JPopupMenu();
popupMenu.add(new JMenuItem("Cut"));
popupMenu.add(new JMenuItem("Copy"));
popupMenu.add(new JMenuItem("Paste"));

// Show on right-click
component.addMouseListener(new MouseAdapter() {
    public void mouseReleased(MouseEvent e) {
        if (e.isPopupTrigger()) {
            popupMenu.show(e.getComponent(), e.getX(), e.getY());
        }
    }
});
```

## Data Display Components

### JTable
Displays data in a tabular format with rows and columns.
```java
String[] columnNames = {"Name", "Age", "City"};
Object[][] data = {
    {"John", 25, "New York"},
    {"Alice", 30, "Boston"},
    {"Bob", 28, "Chicago"}
};
JTable table = new JTable(data, columnNames);
JScrollPane scrollPane = new JScrollPane(table);
```

### JTree
Displays hierarchical data.
```java
DefaultMutableTreeNode root = new DefaultMutableTreeNode("Root");
DefaultMutableTreeNode branch1 = new DefaultMutableTreeNode("Branch 1");
DefaultMutableTreeNode branch2 = new DefaultMutableTreeNode("Branch 2");
DefaultMutableTreeNode leaf1 = new DefaultMutableTreeNode("Leaf 1");
DefaultMutableTreeNode leaf2 = new DefaultMutableTreeNode("Leaf 2");

root.add(branch1);
root.add(branch2);
branch1.add(leaf1);
branch2.add(leaf2);

JTree tree = new JTree(root);
JScrollPane scrollPane = new JScrollPane(tree);
```

### JProgressBar
Displays progress of a task.
```java
JProgressBar progressBar = new JProgressBar(0, 100);
progressBar.setValue(50);
progressBar.setStringPainted(true);
```

## Container and Layout Components

### JScrollPane
Adds scrollbars to a component when needed.
```java
JTextArea textArea = new JTextArea(20, 20);
JScrollPane scrollPane = new JScrollPane(textArea);
scrollPane.setVerticalScrollBarPolicy(JScrollPane.VERTICAL_SCROLLBAR_ALWAYS);
```

### JSplitPane
Divides space between two components with an adjustable divider.
```java
JTextArea leftArea = new JTextArea();
JTextArea rightArea = new JTextArea();
JSplitPane splitPane = new JSplitPane(JSplitPane.HORIZONTAL_SPLIT, 
                                     new JScrollPane(leftArea), 
                                     new JScrollPane(rightArea));
splitPane.setDividerLocation(0.5); // 50% split
```

### JTabbedPane
Displays multiple components in tabs.
```java
JTabbedPane tabbedPane = new JTabbedPane();
tabbedPane.addTab("General", generalPanel);
tabbedPane.addTab("Advanced", advancedPanel);
tabbedPane.addTab("Help", helpPanel);
```

### JToolBar
Container for tool buttons/actions.
```java
JToolBar toolBar = new JToolBar();
toolBar.add(new JButton(new ImageIcon("new.png")));
toolBar.add(new JButton(new ImageIcon("open.png")));
toolBar.addSeparator();
toolBar.add(new JButton(new ImageIcon("save.png")));
frame.add(toolBar, BorderLayout.NORTH);
```

### JLayeredPane
Allows components to overlap with defined z-ordering.
```java
JLayeredPane layeredPane = new JLayeredPane();
JLabel background = new JLabel(new ImageIcon("background.png"));
JLabel foreground = new JLabel(new ImageIcon("foreground.png"));

background.setBounds(0, 0, 800, 600);
foreground.setBounds(100, 100, 400, 300);

layeredPane.add(background, JLayeredPane.DEFAULT_LAYER);
layeredPane.add(foreground, JLayeredPane.PALETTE_LAYER);
```

### JDesktopPane
Container used with JInternalFrames to create MDI applications.
```java
JDesktopPane desktopPane = new JDesktopPane();
JInternalFrame iframe1 = new JInternalFrame("Document 1", true, true, true, true);
iframe1.setSize(300, 200);
iframe1.setVisible(true);
desktopPane.add(iframe1);
frame.add(desktopPane);
```

## Miscellaneous Components

### JOptionPane
Creates standard dialog boxes for messages, confirmations, inputs.
```java
// Message dialog
JOptionPane.showMessageDialog(frame, "Operation completed", "Success", JOptionPane.INFORMATION_MESSAGE);

// Confirmation dialog
int choice = JOptionPane.showConfirmDialog(frame, "Do you want to save?", "Save", JOptionPane.YES_NO_CANCEL_OPTION);

// Input dialog
String name = JOptionPane.showInputDialog(frame, "Enter your name:");
```

### JFileChooser
Dialog for selecting files or directories.
```java
JFileChooser fileChooser = new JFileChooser();
fileChooser.setFileSelectionMode(JFileChooser.FILES_ONLY);
if (fileChooser.showOpenDialog(frame) == JFileChooser.APPROVE_OPTION) {
    File selectedFile = fileChooser.getSelectedFile();
}
```

### JColorChooser
Dialog for selecting colors.
```java
Color selectedColor = JColorChooser.showDialog(frame, "Choose a color", Color.BLUE);
```

### JSeparator
Creates a horizontal or vertical line separator.
```java
JSeparator separator = new JSeparator(JSeparator.HORIZONTAL);
panel.add(separator);
```

### JToolTip
Displays helpful text when the mouse hovers over a component.
```java
JButton button = new JButton("Save");
button.setToolTipText("Save the current document");
```

## Layout Managers

### FlowLayout
Arranges components in a row, wrapping to the next row when needed.
```java
panel.setLayout(new FlowLayout(FlowLayout.LEFT, 10, 10)); // alignment, hgap, vgap
```

### BorderLayout
Arranges components in five regions: North, South, East, West, and Center.
```java
panel.setLayout(new BorderLayout(5, 5)); // hgap, vgap
panel.add(new JButton("North"), BorderLayout.NORTH);
panel.add(new JButton("Center"), BorderLayout.CENTER);
```

### GridLayout
Arranges components in a grid of equal-sized cells.
```java
panel.setLayout(new GridLayout(3, 2, 5, 5)); // rows, cols, hgap, vgap
```

### BoxLayout
Arranges components in a single row or column.
```java
panel.setLayout(new BoxLayout(panel, BoxLayout.Y_AXIS)); // component, axis
```

### CardLayout
Shows one component at a time, like a stack of cards.
```java
CardLayout cardLayout = new CardLayout();
panel.setLayout(cardLayout);
panel.add(firstCard, "FIRST");
panel.add(secondCard, "SECOND");
cardLayout.show(panel, "FIRST"); // Show the first card
```

### GridBagLayout
The most flexible but complex layout manager with fine-grained control.
```java
panel.setLayout(new GridBagLayout());
GridBagConstraints gbc = new GridBagConstraints();

gbc.gridx = 0;
gbc.gridy = 0;
gbc.gridwidth = 2;
gbc.fill = GridBagConstraints.HORIZONTAL;
panel.add(new JTextField(20), gbc);

gbc.gridx = 0;
gbc.gridy = 1;
gbc.gridwidth = 1;
panel.add(new JButton("OK"), gbc);
```

## Event Handling

Swing components use event listeners to handle user interactions:

```java
// ActionListener for buttons, menu items, etc.
button.addActionListener(e -> System.out.println("Button clicked"));

// ItemListener for checkboxes, combo boxes, etc.
checkBox.addItemListener(e -> {
    boolean selected = e.getStateChange() == ItemEvent.SELECTED;
});

// MouseListener for mouse events
component.addMouseListener(new MouseAdapter() {
    public void mouseClicked(MouseEvent e) {
        System.out.println("Clicked at " + e.getX() + ", " + e.getY());
    }
});

// KeyListener for keyboard events
textField.addKeyListener(new KeyAdapter() {
    public void keyPressed(KeyEvent e) {
        if (e.getKeyCode() == KeyEvent.VK_ENTER) {
            System.out.println("Enter pressed");
        }
    }
});

// WindowListener for window events
frame.addWindowListener(new WindowAdapter() {
    public void windowClosing(WindowEvent e) {
        System.out.println("Window closing");
    }
});
```
