# pythone
public class Student {
    private int id;
    private String name;
    private int age;

    public Student(int id, String name, int age) {
        this.id = id;
        this.name = name;
        this.age = age;
    }

    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }
}
import java.util.ArrayList;
import java.util.List;

public class StudentService {
    private List<Student> students = new ArrayList<>();

    public List<Student> getAllStudents() {
        return students;
    }

    public void addStudent(Student student) {
        students.add(student);
    }

    public void deleteStudent(int id) {
        students.removeIf(student -> student.getId() == id);
    }

    public Student getStudentById(int id) {
        for (Student student : students) {
            if (student.getId() == id) {
                return student;
            }
        }
        return null;
    }
}
import random

def print_separator():
    print("-" * 50)

def welcome_message():
    print("Welcome to the Dungeon Adventure!")
    print("You are an adventurer exploring a mysterious dungeon.")
    print("Fight monsters, gather treasures, and try to survive!")
    print_separator()

def get_player_name():
    return input("Enter your name, brave adventurer: ")

class Player:
    def __init__(self, name):
        self.name = name
        self.hp = 100
        self.attack = 15
        self.defense = 10
        self.gold = 0
        self.inventory = []
        self.skills = []
        self.achievements = []
        self.level = 1
        self.floor = 1

    def display_status(self):
        print(f"{self.name} - HP: {self.hp} | Attack: {self.attack} | Defense: {self.defense} | Gold: {self.gold} | Level: {self.level} | Floor: {self.floor}")

    def is_alive(self):
        return self.hp > 0

    def learn_skill(self, skill):
        self.skills.append(skill)
        print(f"You have learned a new skill: {skill}!")

    def earn_achievement(self, achievement):
        if achievement not in self.achievements:
            self.achievements.append(achievement)
            print(f"Achievement unlocked: {achievement}!")

    def use_skill(self, skill, enemy):
        if skill == "Fireball":
            damage = 25
            enemy.hp -= damage
            print(f"You cast Fireball and dealt {damage} damage to {enemy.name}.")
        elif skill == "Heal":
            heal = 20
            self.hp += heal
            print(f"You used Heal and restored {heal} HP.")
        elif skill == "Lightning Strike":
            damage = 35
            enemy.hp -= damage
            print(f"You unleashed Lightning Strike and dealt {damage} damage to {enemy.name}.")
        else:
            print("Unknown skill.")

    def level_up(self):
        self.level += 1
        self.hp += 10
        self.attack += 5
        self.defense += 3
        print(f"Congratulations! You leveled up to Level {self.level}!")

    def ascend_floor(self):
        self.floor += 1
        print(f"You have ascended to Floor {self.floor} of the dungeon.")

class Enemy:
    def __init__(self, name, hp, attack, description="A fearsome foe"):
        self.name = name
        self.hp = hp
        self.attack = attack
        self.description = description

    def is_alive(self):
        return self.hp > 0

    def display_status(self):
        print(f"{self.name} - HP: {self.hp} | Attack: {self.attack}")
        print(self.description)

def create_random_enemy():
    enemy_types = [
        ("Goblin", random.randint(20, 30), random.randint(5, 10), "A sneaky creature with sharp claws."),
        ("Skeleton", random.randint(25, 35), random.randint(8, 12), "A reanimated skeleton wielding a rusty sword."),
        ("Orc", random.randint(30, 40), random.randint(10, 15), "A brutish warrior with a massive axe."),
        ("Troll", random.randint(40, 50), random.randint(10, 20), "A giant troll with immense strength."),
        ("Dark Mage", random.randint(35, 45), random.randint(12, 18), "A sinister sorcerer with dark spells."),
        ("Dragon", random.randint(80, 100), random.randint(20, 30), "A mighty dragon with devastating power.")
    ]
    name, hp, attack, description = random.choice(enemy_types)
    return Enemy(name, hp, attack, description)

def create_random_treasure():
    treasures = [
        {"name": "Gold Coins", "gold": random.randint(10, 50)},
        {"name": "Healing Potion", "hp": 20},
        {"name": "Magic Sword", "attack": 5},
        {"name": "Shield", "defense": 3},
        {"name": "Skill Scroll: Fireball", "skill": "Fireball"},
        {"name": "Skill Scroll: Heal", "skill": "Heal"},
        {"name": "Skill Scroll: Lightning Strike", "skill": "Lightning Strike"},
        {"name": "Treasure Chest", "gold": random.randint(50, 100)}
    ]
    return random.choice(treasures)

def combat(player, enemy):
    print(f"A wild {enemy.name} appears!")
    enemy.display_status()

    while enemy.is_alive() and player.is_alive():
        print_separator()
        print("1. Attack")
        print("2. Use Skill")
        print("3. Run")
        choice = input("Choose your action: ")

        if choice == "1":
            damage = max(1, player.attack - random.randint(0, 5))
            enemy.hp -= damage
            print(f"You dealt {damage} damage to {enemy.name}.")

            if enemy.is_alive():
                enemy_damage = max(1, enemy.attack - random.randint(0, player.defense))
                player.hp -= enemy_damage
                print(f"{enemy.name} dealt {enemy_damage} damage to you.")
            else:
                print(f"You defeated the {enemy.name}!")
                player.earn_achievement(f"Defeated {enemy.name}")
                player.level_up()
        elif choice == "2":
            if player.skills:
                print("Available skills:")
                for i, skill in enumerate(player.skills):
                    print(f"{i + 1}. {skill}")
                skill_choice = int(input("Choose a skill: ")) - 1
                if 0 <= skill_choice < len(player.skills):
                    player.use_skill(player.skills[skill_choice], enemy)
                else:
                    print("Invalid skill choice.")
            else:
                print("You have no skills to use.")
        elif choice == "3":
            if random.random() < 0.5:
                print("You successfully escaped!")
                return
            else:
                print("You failed to escape!")
                enemy_damage = max(1, enemy.attack - random.randint(0, player.defense))
                player.hp -= enemy_damage
                print(f"{enemy.name} dealt {enemy_damage} damage to you.")
        else:
            print("Invalid choice.")

        player.display_status()

    if not player.is_alive():
        print("You have fallen in battle. Game over.")

def find_treasure(player):
    treasure = create_random_treasure()
    print(f"You found a treasure: {treasure['name']}!")

    if "gold" in treasure:
        player.gold += treasure["gold"]
        print(f"You gained {treasure['gold']} gold.")
    elif "hp" in treasure:
        player.hp += treasure["hp"]
        print(f"You restored {treasure['hp']} HP.")
    elif "attack" in treasure:
        player.attack += treasure["attack"]
        print(f"Your attack increased by {treasure['attack']}.")
    elif "defense" in treasure:
        player.defense += treasure["defense"]
        print(f"Your defense increased by {treasure['defense']}.")
    elif "skill" in treasure:
        player.learn_skill(treasure["skill"])

    player.display_status()

def special_event(player):
    events = [
        "You encounter a wise sage who offers to teach you a skill.",
        "You find a hidden spring that restores all your health.",
        "A trap is triggered, and you take damage.",
        "You meet a merchant offering rare items.",
        "You stumble upon an ancient relic that boosts your stats.",
        "A hidden door leads to a treasure-filled chamber.",
        "A powerful blessing increases your stats temporarily.",
        "An injured traveler shares a secret about the dungeon."
    ]
    event = random.choice(events)
    print(event)

    if "skill" in event:
        new_skill = random.choice(["Fireball", "Heal", "Lightning Strike"])
        player.learn_skill(new_skill)

    if "spring" in event:
        player.hp = 100
        print("Your health is fully restored!")

    if "trap" in event:
        damage = random.randint(10, 20)
        player.hp -= damage
        print(f"The trap dealt {damage} damage to you.")

    if "merchant" in event:
        item = random.choice(["Healing Potion", "Magic Sword", "Shield"])
        cost = random.randint(10, 50)
        print(f"The merchant offers a {item} for {cost} gold.")
        if player.gold >= cost:
            print("You bought the item.")
            player.inventory.append(item)
            player.gold -= cost
        else:
            print("You don't have enough gold.")

def main():
    welcome_message()
    player_name = get_player_name()
    player = Player(player_name)

    while player.is_alive():
        print_separator()
        print("1. Explore the dungeon")
        print("2. Check your status")
        print("3. Rest")
        choice = input("What do you want to do? ")

        if choice == "1":
            encounter = random.choice(["enemy", "treasure", "event"])
            if encounter == "enemy":
                enemy = create_random_enemy()
                combat(player, enemy)
            elif encounter == "treasure":
                find_treasure(player)
            elif encounter == "event":
                special_event(player)

        elif choice == "2":
            player.display_status()

        elif choice == "3":
            player.hp += 10
            print("You rest and recover 10 HP.")

        else:
            print("Invalid choice.")

    print("Game over.")

if __name__ == "__main__":
    main()
    import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

@WebServlet("/students")
public class StudentServlet extends HttpServlet {
    private StudentService studentService = new StudentService();

    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        String action = request.getParameter("action");
        if (action == null) action = "list";

        switch (action) {
            case "list":
                request.setAttribute("students", studentService.getAllStudents());
                request.getRequestDispatcher("index.jsp").forward(request, response);
                break;
            case "add":
                request.getRequestDispatcher("add-student.jsp").forward(request, response);
                break;
            case "delete":
                int id = Integer.parseInt(request.getParameter("id"));
                studentService.deleteStudent(id);
                response.sendRedirect("students");
                break;
            default:
                response.getWriter().println("Invalid action");
        }
    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        String name = request.getParameter("name");
        int age = Integer.parseInt(request.getParameter("age"));
        int id = studentService.getAllStudents().size() + 1;

        Student student = new Student(id, name, age);
        studentService.addStudent(student);

        response.sendRedirect("students");
    }
}
<!DOCTYPE html>
<html>
<head>
    <title>Student Management</title>
</head>
<body>
    <h1>Student List</h1>
    <a href="students?action=add">Add New Student</a>
    <table border="1">
        <tr>
            <th>ID</th>
            <th>Name</th>
            <th>Age</th>
            <th>Actions</th>
        </tr>
        <c:forEach var="student" items="${students}">
            <tr>
                <td>${student.id}</td>
                <td>${student.name}</td>
                <td>${student.age}</td>
                <td>
                    <a href="students?action=delete&id=${student.id}">Delete</a>
                </td>
            </tr>
        </c:forEach>
    </table>
</body>
</html>
<!DOCTYPE html>
<html>
<head>
    <title>Add Student</title>
</head>
<body>
    <h1>Add Student</h1>
    <form action="students" method="post">
        <label for="name">Name:</label>
        <input type="text" name="name" required><br>
        <label for="age">Age:</label>
        <input type="number" name="age" required><br>
        <button type="submit">Add</button>
    </form>
</body>
</html>
import java.util.ArrayList;
import java.util.List;

public class StudentService {
    private List<Student> students = new ArrayList<>();

    public List<Student> getAllStudents() {
        return students;
    }

    public void addStudent(Student student) {
        students.add(student);
    }

    public void deleteStudent(int id) {
        students.removeIf(student -> student.getId() == id);
    }

    public Student getStudentById(int id) {
        for (Student student : students) {
            if (student.getId() == id) {
                return student;
            }
        }
        return null;
    }

    public void updateStudent(int id, String name, int age) {
        Student student = getStudentById(id);
        if (student != null) {
            student.setName(name);
            student.setAge(age);
        }
    }
}
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

@WebServlet("/students")
public class StudentServlet extends HttpServlet {
    private StudentService studentService = new StudentService();

    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        String action = request.getParameter("action");
        if (action == null) action = "list";

        switch (action) {
            case "list":
                response.getWriter().println("Student List:");
                for (Student student : studentService.getAllStudents()) {
                    response.getWriter().println(student);
                }
                break;
            case "add":
                response.getWriter().println("To add a student, send a POST request.");
                break;
            case "delete":
                int id = Integer.parseInt(request.getParameter("id"));
                studentService.deleteStudent(id);
                response.getWriter().println("Student deleted.");
                break;
            case "update":
                response.getWriter().println("To update a student, send a POST request with 'update' action.");
                break;
            default:
                response.getWriter().println("Invalid action.");
        }
    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        String action = request.getParameter("action");
        if ("add".equals(action)) {
            String name = request.getParameter("name");
            int age = Integer.parseInt(request.getParameter("age"));
            int id = studentService.getAllStudents().size() + 1;

            Student student = new Student(id, name, age);
            studentService.addStudent(student);

            response.getWriter().println("Student added: " + student);
        } else if ("update".equals(action)) {
            int id = Integer.parseInt(request.getParameter("id"));
            String name = request.getParameter("name");
            int age = Integer.parseInt(request.getParameter("age"));

            studentService.updateStudent(id, name, age);
            response.getWriter().println("Student updated: " + studentService.getStudentById(id));
        } else {
            response.getWriter().println("Invalid POST action.");
        }
    }
}
