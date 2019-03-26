import requests
from bs4 import BeautifulSoup


class Api:

    def __init__(self, house):
        """
        :param house: house to collect data
        """
        self.houses = {"Wohnanlage Tarforst - Haus I": {
            "washer_quantity": 4,
            "id_dryer": 1,
            "id_washer": 1
        },
            "Wohnanlage Tarforst - Haus IV": {
                "washer_quantity": 3,
                "id_dryer": 2,
                "id_washer": 2
            },
            "Wohnanlage Tarforst - Haus VIII": {
                "washer_quantity": 2,
                "id_dryer": 3,
                "id_washer": 3
            },
            "Wohnanlage Kleeburger Weg": {
                "washer_quantity": 6,
                "id_dryer": 7,
                "id_washer": 6
            },
            "Wohnanlage Petrisberg": {
                "washer_quantity": 5,
                "id_dryer": 11,
                "id_washer": 10
            },
            "Wohnanlage Martinskloster": {
                "washer_quantity": 3,
                "id_dryer": 9,
                "id_washer": 9
            },
            "Wohnanlage Olewig": {
                "washer_quantity": 4,
                "id_dryer": 8,
                "id_washer": 8
            }
        }
        self.house = house
        site = requests.get("http://app-in-den-keller.de/cgi-bin/wm")
        self.soup = BeautifulSoup(site.text, "html.parser").findAll("list")
        self.same_id = self.houses[self.house]["id_washer"] == self.houses[self.house]["id_dryer"]

    @property
    def all_washers(self):
        """
        :return: dict containing all washers with their machine ID and their time
        """
        id_washer = self.houses[self.house]["id_washer"]
        washer_quantity = self.houses[self.house]["washer_quantity"]
        output = {}
        for list_content in self.soup:
            html_washer_id = list_content.contents[3].contents[0]
            if html_washer_id == str(id_washer):
                html_machine_id = list_content.contents[0].contents[0]
                html_machine_time = list_content.contents[1].contents[0]
                if not self.same_id:
                    output[html_machine_id] = html_machine_time
                else:
                    if self.house == "Wohnanlage Martinskloster":
                        if int(html_machine_id) > 2:
                            output[html_machine_id] = html_machine_time
                    elif self.house == "Wohnanlage Tarforst - Haus VIII":
                        if int(html_machine_id) <= washer_quantity or int(html_machine_id) == 5:
                            output[html_machine_id] = html_machine_time
                    else:
                        if int(html_machine_id) <= washer_quantity:
                            output[html_machine_id] = html_machine_time
        return output

    @property
    def all_dryers(self):
        """
        :return: dict containing all dryers with their machine ID and their time
        """
        id_dryer = self.houses[self.house]["id_dryer"]
        washer_quantity = self.houses[self.house]["washer_quantity"]
        output = {}
        for list_content in self.soup:
            html_dryer_id = list_content.contents[3].contents[0]
            if html_dryer_id == str(id_dryer):
                html_machine_id = list_content.contents[0].contents[0]
                html_machine_time = list_content.contents[1].contents[0]
                if not self.same_id:
                    output[html_machine_id] = html_machine_time
                else:
                    if self.house == "Wohnanlage Tarforst - Haus IV":
                        if int(html_machine_id) == 4:
                            output[html_machine_id] = html_machine_time
                    elif self.house == "Wohnanlage Martinskloster":
                        if int(html_machine_id) <= 2:
                            output[html_machine_id] = html_machine_time
                    else:
                        if int(html_machine_id) > washer_quantity:
                            output[html_machine_id] = html_machine_time
        return output

    @property
    def all_machines(self):
        """
        :return: dict containing all washers with times in one dict and all dryers with times in another dict
        """
        return {"washers": self.all_washers, "dryers": self.all_dryers}

    @property
    def all_available_washers(self):
        """
        :return: tuple containing all washers which aren't running with their ID
        """
        id_washer = self.houses[self.house]["id_washer"]
        washer_quantity = self.houses[self.house]["washer_quantity"]
        output = []
        for list_content in self.soup:
            html_washer_id = list_content.contents[3].contents[0]
            if html_washer_id == str(id_washer):
                html_machine_id = list_content.contents[0].contents[0]
                html_machine_running = list_content.contents[2].contents[0]
                if not self.same_id:
                    if not html_machine_running == "true":
                        output.append(html_machine_id)
                else:
                    if self.house == "Wohnanlage Martinskloster":
                        if int(html_machine_id) > 2:
                            if not html_machine_running == "true":
                                output.append(html_machine_id)
                    elif self.house == "Wohnanlage Tarforst - Haus VIII":
                        if int(html_machine_id) <= washer_quantity or int(html_machine_id) == 5:
                            if not html_machine_running == "true":
                                output.append(html_machine_id)
                    else:
                        if int(html_machine_id) <= washer_quantity:
                            if not html_machine_running == "true":
                                output.append(html_machine_id)
        return tuple(output)

    @property
    def all_available_dryers(self):
        """
        :return: tuple containing all dryers which aren't running with their ID
        """
        id_dryer = self.houses[self.house]["id_dryer"]
        washer_quantity = self.houses[self.house]["washer_quantity"]
        output = []
        for list_content in self.soup:
            html_dryer_id = list_content.contents[3].contents[0]
            if html_dryer_id == str(id_dryer):
                html_machine_id = list_content.contents[0].contents[0]
                html_machine_running = list_content.contents[2].contents[0]
                if not self.same_id:
                    if not html_machine_running == "true":
                        output.append(html_machine_id)
                else:
                    if self.house == "Wohnanlage Tarforst - Haus IV":
                        if int(html_machine_id) == 4:
                            if not html_machine_running == "true":
                                output.append(html_machine_id)
                    elif self.house == "Wohnanlage Martinskloster":
                        if int(html_machine_id) <= 2:
                            if not html_machine_running == "true":
                                output.append(html_machine_id)
                    else:
                        if int(html_machine_id) > washer_quantity:
                            if not html_machine_running == "true":
                                output.append(html_machine_id)
        return tuple(output)