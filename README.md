# EntertainmentAttendance
## A simple program which allows attendance and ticket data to be collected for different entertainment formats.

### create the ticket and attendants class
    class Ticket:
        def __init__(self, kind, cost):
            self.kind = kind
            self.cost = cost
    
    
    class Attendants:
        def __init__(self, name, type_ticket, seat_numbers, age):
            self.type_t = type_ticket
            self.seat_num = seat_numbers
            self.name = name
            self.age = age
    
    
### here we check to see if any attraction is at max capacity
    def proper_entrance(self, group):
        if len(self.attendants) + len(group.name) < self.max_seating:
            for people in group.name:
                self.attendants.append(people)
            self.passes.append(group.type_t)
            for seats in group.seat_num:
                self.seats.append(seats)
        else:
            print("Max Capacity")
    
    
### we create our parent class, entertainment, which contacts functions to add an attendant, give the number of attendants in an attraction, declare revenue from tickets, and list which seats have been taken
    class Entertainment:
        def __init__(self, attraction, max_seating):
            self.att = attraction
            self.attendants = []
            self.passes = []
            self.seats = []
            self.max_seating = max_seating
    
        def add_attend(self, group):
            if len(self.attendants) + len(group.name) < self.max_seating:
                for people in group.name:
                    self.attendants.append(people)
                self.passes.append(group.type_t)
                for seats in group.seat_num:
                    self.seats.append(seats)
            else:
                print("Max Capacity")
    
        def num_attend(self):
            print(len(self.attendants))
            return len(self.attendants)
    
        def revenue(self):
            revenue = 0
            for ticket in self.passes:
                revenue += ticket.cost
            print(revenue)
            return revenue
    
        def seats_taken(self):
            seats_taken = []
            for seats in self.seats:
                seats_taken.append(seats)
            print(seats_taken)
    
    
    class Carnival(Entertainment):
        def profit(self):
            profit = 0
            for ticket in self.passes:
                if ticket == family_pass:
                    profit += ticket.cost - 16
                elif ticket == couples_pass:
                    profit += ticket.cost - 8
                elif ticket == single_pass:
                    profit += ticket.cost - 4
            print(profit)
            return profit

### small safety warning for anyone who doesn't know not to pet lions. Can be editted to fit any "R" rated movie warnings.
        @staticmethod
        def safety_warning(item):
            if item == "lions":
                print("please do not pet the lions")
            else:
                pass
    
### Here we append an attribute, as movies need ratings.
    class MovieTheater(Entertainment):
        def __init__(self, attraction, max_seating, rating):
            Entertainment.__init__(self, attraction, max_seating)
            self.rating = rating
    
        def profit(self):
            profit = 0
            for ticket in self.passes:
                if ticket == movie_couple:
                    profit += ticket.cost - 4
                elif ticket == movie_ticket:
                    profit += ticket.cost - 2
                elif ticket == movie_group:
                    profit += ticket.cost - 8
            print(profit)
            return profit
            
### Our add attendants needed some shaping as not everyone can see every movie. Our attendants have a list of ages per group, and our rating is based off of those ages.
        def add_attend(self, group):
            if self.rating.lower() == "r":
                if max(group.age) < 18:
                    print("Do not admit")
                else:
                    proper_entrance(self, group)
            elif self.rating.lower() == "pg-13":
                group.age.sort()
                if group.age[0] < 13:
                    print("Do not admit")
                else:
                    proper_entrance(self, group)
    
### Sample Inputs
    family_pass = Ticket(4, 20.00)
    couples_pass = Ticket(2, 12.00)
    single_pass = Ticket(1, 7.00)
    
    movie_ticket = Ticket(1, 6.00)
    movie_couple = Ticket(2, 11.00)
    movie_group = Ticket(4, 18)
    
    a1 = Attendants(["jessie", 'james', 'juan', 'kelly'], family_pass, [11, 12, 13, 14], [20, 21, 20, 19])
    a2 = Attendants(["mark", 'sam'], couples_pass, [3, 4], [16, 15])
    a3 = Attendants("maria", single_pass, [6], 50)
    
    infinitywar = MovieTheater("infinitywar", 100, "r")
