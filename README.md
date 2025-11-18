public class Player
{
    public string PlayerId { get; private set; }
    public int Coins { get; private set; }

    public Player(string id)
    {
        PlayerId = id;
        Coins = 0;
    }

    public void AddCoins(int amount)
    {
        Coins += amount;
    }

    public bool SpendCoins(int amount)
    {
        if (Coins >= amount)
        {
            Coins -= amount;
            return true;
        }
        return false;
    }
}

public class CoinManager
{
    private Dictionary<string, Player> players = new Dictionary<string, Player>();

    public void RegisterPlayer(string playerId)
    {
        if (!players.ContainsKey(playerId))
        {
            players[playerId] = new Player(playerId);
        }
    }

    public void CollectCoin(string playerId, int amount)
    {
        if (players.ContainsKey(playerId))
        {
            players[playerId].AddCoins(amount);
        }
    }

    public bool Purchase(string playerId, int cost)
    {
        if (players.ContainsKey(playerId))
        {
            return players[playerId].SpendCoins(cost);
        }
        return false;
    }

    public int GetPlayerCoins(string playerId)
    {
        return players.ContainsKey(playerId) ? players[playerId].Coins : 0;
    }
}
