//controller
import java.sql.*;
import java.util.ArrayList;
import java.util.List;

public class ContatosController {

    public List<Contatos> listarContatos() {
        List<Contatos> contatos = new ArrayList<>();

        try {
            Connection conn = Database.getConnection();
            String sql = "SELECT * FROM contatos";
            Statement stmt = conn.createStatement();
            ResultSet rs = stmt.executeQuery(sql);

            while (rs.next()) {
                Contatos c = new Contatos(
                    rs.getInt("id"),
                    rs.getString("nome"),
                    rs.getString("telefone"),
                    rs.getString("email")
                );
                contatos.add(c);
            }

            rs.close();
            stmt.close();
            conn.close();

        } catch (Exception e) {
            e.printStackTrace();
        }

        return contatos;
    }
}

//view
package View;

import Model.Contatos;
import java.util.List;

public class ContatosView {

    public void mostrarContatos(List<Contatos> contatos) {
        System.out.println("=== Lista de Contatos ===");
        for (Contatos c : contatos) {
            System.out.println(c);
        }
    }
}
