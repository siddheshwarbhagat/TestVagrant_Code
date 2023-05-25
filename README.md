import java.util.HashMap;
import java.util.Map;
import java.util.ArrayList;
import java.util.List;
import java.util.Scanner;

public class Subscriptions {
    static final Map<String, Map<String, Double>> DailyPrices = new HashMap<>();
    static void DailyPrices() {
        Map<String, Double> toiPrices = new HashMap<>();
        toiPrices.put("Monday", 3.0);
        toiPrices.put("Tuesday", 3.0);
        toiPrices.put("Wednesday", 3.0);
        toiPrices.put("Thursday", 3.0);
        toiPrices.put("Friday", 3.0);
        toiPrices.put("Saturday", 5.0);
        toiPrices.put("Sunday", 6.0);

        Map<String, Double> hinduPrices = new HashMap<>();
        hinduPrices.put("Monday", 2.5);
        hinduPrices.put("Tuesday", 2.5);
        hinduPrices.put("Wednesday", 2.5);
        hinduPrices.put("Thursday", 2.5);
        hinduPrices.put("Friday", 2.5);
        hinduPrices.put("Saturday", 4.0);
        hinduPrices.put("Sunday", 4.0);

        Map<String, Double> etPrices = new HashMap<>();
        etPrices.put("Monday", 4.0);
        etPrices.put("Tuesday", 4.0);
        etPrices.put("Wednesday", 4.0);
        etPrices.put("Thursday", 4.0);
        etPrices.put("Friday", 4.0);
        etPrices.put("Saturday", 4.0);
        etPrices.put("Sunday", 10.0);

        Map<String, Double> bmPrices = new HashMap<>();
        bmPrices.put("Monday", 1.5);
        bmPrices.put("Tuesday", 1.5);
        bmPrices.put("Wednesday", 1.5);
        bmPrices.put("Thursday", 1.5);
        bmPrices.put("Friday", 1.5);
        bmPrices.put("Saturday", 1.5);
        bmPrices.put("Sunday", 1.5);

        Map<String, Double> htPrices = new HashMap<>();
        htPrices.put("Monday", 2.0);
        htPrices.put("Tuesday", 2.0);
        htPrices.put("Wednesday", 2.0);
        htPrices.put("Thursday", 2.0);
        htPrices.put("Friday", 2.0);
        htPrices.put("Saturday", 4.0);
        htPrices.put("Sunday", 4.0);

        DailyPrices.put("TOI", toiPrices);
        DailyPrices.put("Hindu", hinduPrices);
        DailyPrices.put("ET", etPrices);
        DailyPrices.put("BM", bmPrices);
        DailyPrices.put("HT", htPrices);
    }
    static List<List<String>> calculateWeeklySubscriptionExpenses(double budget) {
        List<List<String>> combinations = new ArrayList<>();
        for (String newspaper1 : DailyPrices.keySet()) {
            for (String newspaper2 : DailyPrices.keySet()) {
                if (!newspaper1.equals(newspaper2)) {
                    double total = calculateTotalPrice(newspaper1) + calculateTotalPrice(newspaper2);
                    if (total <= budget) {
                        List<String> combination = new ArrayList<>();
                        combination.add(newspaper1);
                        combination.add(newspaper2);
                        combinations.add(combination);
                    }
                }
            }
        }
        return combinations;
    }
    static double calculateTotalPrice(String newspaper) {
        Map<String, Double> prices = DailyPrices.get(newspaper);
        double totalPrice = 0.0;
        for (double price : prices.values()) {
            totalPrice += price;
        }
        return totalPrice;
    }
    public static void main(String[] args) {
        DailyPrices();

        System.out.print("Enter weekly budget: ");
        Scanner scanner = new Scanner(System.in);
        double weeklyBudget = scanner.nextDouble();

        List<List<String>> combinations = calculateWeeklySubscriptionExpenses(weeklyBudget);

        for (List<String> combination : combinations) {
            System.out.println(combination);
        }
    }
}
