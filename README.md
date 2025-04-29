DROP TABLE IF EXISTS matriculas;
DROP TABLE IF EXISTS alunos;
DROP TABLE IF EXISTS cursos;

CREATE TABLE alunos (
  id SERIAL PRIMARY KEY,
  nome TEXT NOT NULL,
  turma TEXT NOT NULL,
  data_nascimento DATE
);

CREATE TABLE cursos (
  id SERIAL PRIMARY KEY,
  nome TEXT NOT NULL,
  duracao_anos INT
);

CREATE TABLE matriculas (
  id SERIAL PRIMARY KEY,
  aluno_id INT REFERENCES alunos(id) ON DELETE CASCADE,
  curso_id INT REFERENCES cursos(id) ON DELETE CASCADE,
  data_matricula DATE DEFAULT CURRENT_DATE
);

INSERT INTO alunos (nome, turma, data_nascimento)
VALUES 
('Ana Lima', '1B', '2002-05-10'),
('Bruno Souza', '1B', '2003-08-15'),
('Pedro Jorge', '1B', '2006-05-10'),
('Humberto Filho', '1B', '2006-05-10'),
('Maria Vitoria', '1B', '2006-05-10'),
('Adriana Policia', '1B', '2006-05-10'),
('Rafael Gomes', '1B', '2006-05-10'),
('Vinicius Ciargi', '1B', '2006-05-10'),
('Enzo Rezende', '1B', '2006-05-10'),
('Matheus Scapolan', '1B', '2006-05-10');

INSERT INTO cursos (nome, duracao_anos)
VALUES 
('Engenharia de Software', 4),
('Administração', 4),
('Engenharia de Computação', 5);

INSERT INTO matriculas (aluno_id, curso_id)
VALUES
(1,1),
(2,2),
(3,2),
(4,3),
(5,1),
(6,3),
(7,3),
(8,2),
(9,1),
(10,2);

SELECT 
  a.nome AS aluno,
  c.nome AS curso,
  m.data_matricula
FROM matriculas m
JOIN alunos a ON m.aluno_id = a.id
JOIN cursos c ON m.curso_id = c.id;
