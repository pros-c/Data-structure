package PlagiarismDetectionSystem;
import java.awt.*;
import java.awt.event.*;
import java.io.*;
import java.util.HashMap;
import javax.swing.*;

public class PlagiarismDetectionSystem extends Frame {
    HashMap<String, String> documents = new HashMap<>();

    public PlagiarismDetectionSystem() {
        Label docLabel = new Label("Upload Document:");
        Button uploadButton = new Button("Upload");
        TextArea resultArea = new TextArea("Plagiarism Detection Results...");
        resultArea.setEditable(false);
        setLayout(new FlowLayout());
        add(docLabel);
        add(uploadButton);
        add(resultArea);

        uploadButton.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                FileDialog fileDialog = new FileDialog((Frame) null, "Select Document to Upload");
                fileDialog.setMode(FileDialog.LOAD);
                fileDialog.setVisible(true);
                String fileName = fileDialog.getFile();
                if (fileName != null) {
                    String filePath = fileDialog.getDirectory() + fileName;
                    String documentText = readFile(filePath);
                    String processedText = preprocessText(documentText);
                    documents.put(fileName, processedText);
                    String results = detectPlagiarism(processedText);
                    resultArea.setText(results);
                }
            }
        });

        addWindowListener(new WindowAdapter() {
            public void windowClosing(WindowEvent we) {
                System.exit(0);
            }
        });

        setTitle("Plagiarism Detection System");
        setSize(400, 400);
        setVisible(true);
        setBackground(Color.CYAN);
    }

    private String readFile(String filePath) {
        StringBuilder content = new StringBuilder();
        try {
            BufferedReader br = new BufferedReader(new FileReader(filePath));
            String line;
            while ((line = br.readLine()) != null) {
                content.append(line).append("\n");
            }
            br.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
        return content.toString();
    }

    private String preprocessText(String text) {
        return text;
    }

    private String detectPlagiarism(String text) {

        return "No plagiarism detected.";
    }

    public static void main(String[] args) {
    	new PlagiarismDetectionSystem();
   
    }
}
