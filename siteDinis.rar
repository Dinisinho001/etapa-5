<?php
include_once "LigarBD.php";

// Handle insert operation
if (isset($_POST['insert'])) {
    $nome = $_POST['nome'];
    $qt_seguidores = $_POST['qt_seguidores'];

    $sql = "INSERT INTO artista (nome, qt_seguidores) VALUES (?, ?)";
    $stmt = $conn->prepare($sql);
    $stmt->bind_param("si", $nome, $qt_seguidores);
    if ($stmt->execute()) {
        echo "Novo artista adicionado com sucesso";
    } else {
        echo "Error: " . $stmt->error;
    }
    $stmt->close();
}

// Handle update operation
if (isset($_POST['update'])) {
    $id = $_POST['id'];
    $nome = $_POST['nome'];
    $qt_seguidores = $_POST['qt_seguidores'];

    $sql = "UPDATE artista SET nome=?, qt_seguidores=? WHERE id=?";
    $stmt = $conn->prepare($sql);
    $stmt->bind_param("sii", $nome, $qt_seguidores, $id);
    if ($stmt->execute()) {
        echo "Atializado com sucesso";
    } else {
        echo "Error: " . $stmt->error;
    }
    $stmt->close();
}

// Handle delete operation
if (isset($_POST['delete'])) {
    $id = $_POST['id'];

    $sql = "DELETE FROM artista WHERE id=?";
    $stmt = $conn->prepare($sql);
    $stmt->bind_param("i", $id);
    if ($stmt->execute()) {
        echo "Deletado com sucesso";
    } else {
        echo "Error: " . $stmt->error;
    }
    $stmt->close();
}

// Fetch and display data
$result = $conn->query("SELECT id, nome, qt_seguidores FROM artista");
?>
<!DOCTYPE html>
<html lang="en">

<head>

    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta email="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">

    <title>Inserir Artista</title>
    <link rel="stylesheet" href="http://cdn.datatables.net/2.0.7/css/dataTables.dataTables.min.css">
    <!-- Custom fonts for this template-->
    <link href="../vendor/fontawesome-free/css/all.min.css" rel="stylesheet" type="text/css">
    <link href="https://fonts.googleapis.com/css?family=Nunito:200,200i,300,300i,400,400i,600,600i,700,700i,800,800i,900,900i" rel="stylesheet">

    <!-- Custom styles for this template-->
    <link href="../css/sb-admin-2.min.css" rel="stylesheet">


</head>

<body id="page-top">

    <!-- Page Wrapper -->
    <div id="wrapper">

        <?php require_once "partials/sidebar.php"; ?>

        <!-- Content Wrapper -->
        <div id="content-wrapper" class="d-flex flex-column">

            <!-- Main Content -->
            <div id="content">

                <!-- Begin Page Content -->
                <div class="container-fluid">
                    <?php
                    require_once "partials/msg_sucesso.php";
                    require_once "partials/msg_erros.php";
                    ?>
                    <!-- Page Heading -->
                    <div class="d-sm-flex align-items-center justify-content-between mb-4">
                        <h1 class="h3 mb-0 text-gray-800">Inserir Artistas</h1>
                    </div>

                        <tbody>
                            <form method="POST">
                                <label for="nome">Name:</label>
                                <input type="text" id="nome" name="nome" required>
                                <label for="qt_seguidores">Seguidores:</label>
                                <input type="number" id="qt_seguidores" name="qt_seguidores" required>
                                <button type="submit" name="insert">Inserir</button>
                            </form>
                        </tbody>

                    <div>
                        <div class="d-sm-flex align-items-center justify-content-between mb-4">
                            <h3>Ver Lista</h3>
                        </div>
                        <table id="tabelaArtista">
                            <thead>
                                <tr>
                                    <th>Name</th>
                                    <th>Seguidores</th>
                                    <th>Edições</th>
                                </tr>
                            </thead>
                            <tbody>
                                <?php while ($row = $result->fetch_assoc()) : ?>
                                    <tr>
                                        <td><?= $row["nome"] ?></td>
                                        <td><?= $row["qt_seguidores"] ?></td>
                                        <td>
                                            <!-- Update form within the table row -->
                                            <form method="POST" style="display:inline;">
                                                <input type="hidden" name="id" value="<?= $row["id"] ?>">
                                                <input type="text" name="nome" value="<?= $row["nome"] ?>" required>
                                                <input type="number" name="qt_seguidores" value="<?= $row["qt_seguidores"] ?>" required>
                                                <button type="submit" name="update">Editar</button>
                                            </form>
                                            <!-- Delete form within the table row -->
                                            <form method="POST" style="display:inline;">
                                                <input type="hidden" name="id" value="<?= $row["id"] ?>">
                                                <button type="submit" name="delete">Apagar</button>
                                            </form>
                                        </td>
                                    </tr>
                                <?php endwhile; ?>
                            </tbody>
                        </table>
                    </div>

                </div>
                <!-- /.container-fluid -->
            </div>
            <!-- End of Main Content -->

            <?php require_once "partials/footer.php"; ?>


        </div>
        <!-- End of Content Wrapper -->

    </div>
    <!-- End of Page Wrapper -->

    <!-- Scroll to Top Button-->
    <a class="scroll-to-top rounded" href="#page-top">
        <i class="fas fa-angle-up"></i>
    </a>

    <?php require_once "partials/modal_logout.php"; ?>

    <!-- Bootstrap core JavaScript-->
    <script src="../vendor/jquery/jquery.min.js"></script>
    <script src="http://cdn.datatables.net/2.0.7/js/dataTables.min.js"></script>
    <script src="../vendor/bootstrap/js/bootstrap.bundle.min.js"></script>

    <!-- Core plugin JavaScript-->
    <script src="../vendor/jquery-easing/jquery.easing.min.js"></script>

    <!-- Custom scripts for all pages-->
    <script src="../js/sb-admin-2.min.js"></script>
    <script>
        $(document).ready(function() {
            $('#tabelaArtista').DataTable({
                "language": {
                    "sProcessing": "Em processamento...",
                    "sLengthMenu": "Mostrar _MENU_ registos",
                    "sZeroRecords": "Nenhum resultado encontrado",
                    "sEmptyTable": "Não há dados disponíveis nesta tabela",
                    "sInfo": "Mostrando registos de _START_ a _END_ de um total de _TOTAL_ registos",
                    "sInfoEmpty": "Mostrando registos de 0 a 0 de um total de 0 registos",
                    "sInfoFiltered": "(filtrando um total de _MAX_ registos)",
                    "sInfoPostFix": "",
                    "sSearch": "Pesquisar:",
                    "sUrl": "",
                    "sInfoThousands": ",",
                    "sLoadingRecords": "Carregando...",
                    "oAria": {
                        "sSortAscending": ": Ative para classificar a coluna em ordem crescente",
                        "sSortDescending": ": Ative para classificar a coluna em ordem decrescente"
                    }
                }
            });
        });
    </script>
</body>
</html>
